# Pdf Chunking Retry System

This .NET Core 5 project implements a scalable and fault-tolerant PDF generation system using chunking and retry logic. It is designed to generate large PDFs (up to 1500+ pages) by breaking them into manageable parts, handling failures gracefully, and merging them at the end.

---

## 📌 Features

- IronPDF-based generation
- JSON request handling
- Azure Blob Storage integration
- Chunking PDF generation (based on hazards/compliance)
- Retry failed chunks
- Merge final PDF

---

## 🏗️ Architecture Overview

```text
Angular ➝ .NET Core API ➝ Save JSON to Azure Blob ➝ Send Queue to Service Bus ➝
Workflow Microservice ➝ Read JSON ➝ Chunk PDF Generation ➝ Retry Failed ➝ Merge PDFs ➝ Upload Final PDF
```

---

## 📂 Project Structure

```
/ComplexPdfProcessor.API
  Controllers/
    PdfRequestController.cs        // Initiates PDF request
    PdfProcessingController.cs     // Simulates worker/microservice
  Program.cs
  Startup.cs

/ComplexPdfProcessor.Application
  Services/
    Interfaces/
      IPdfChunkService.cs          // Interface for chunk logic
      IPdfGenerationService.cs     // Interface for generation
      IStorageService.cs           // Interface for blob
      IRetryService.cs             // Interface for retry logic
    Implementations/
      PdfChunkService.cs           // Splits and merges chunks
      PdfGenerationService.cs      // Uses IronPDF
      AzureBlobStorageService.cs   // Blob implementation
      RetryService.cs              // Retry failed chunks

  Models/
    PdfRequestDto.cs               // JSON model
    PdfChunk.cs                    // Each chunk
    PdfGenerationResult.cs        // Result per chunk

/ComplexPdfProcessor.Tests
  PdfChunkServiceTests.cs         // Unit tests for chunking
  RetryServiceTests.cs            // Unit tests for retry

/ComplexPdfProcessor.sln
```

---

## 🧪 Unit Tests

Located in `/ComplexPdfProcessor.Tests`, powered by xUnit:

### ✅ PdfChunkServiceTests.cs
- Tests chunk creation based on hazard/compliance
- Verifies order of sections/subsections/questions

### 🔁 RetryServiceTests.cs
- Tests retry logic for failed chunks
- Mocks PDF generation failures and successful retries

---

## 🧑‍💻 Sample Endpoints

### 1. `POST /api/pdf-request`
Initiate a new PDF generation request
```json
{
  "project_id": "1",
  "project_name": "Safety Audit",
  "machine_data": [ ... ]
}
```

### 2. `POST /api/pdf-process/{tid}`
Workflow service processes the PDF request

### 3. `GET /api/pdf/status/{tid}`
Check status of processing (Success, InProgress, Failed)

---

## 🛠️ Tech Stack
- .NET Core 5
- IronPDF
- Azure Blob Storage
- xUnit (testing)
- Swashbuckle for Swagger UI
- Newtonsoft.Json

---

## 🔗 Postman Collection
A sample Postman collection is included in the `/Postman` folder for testing endpoints:

- `ComplexPdf.postman_collection.json`

---

## ✅ To Do
- [x] Chunking logic
- [x] Retry mechanism
- [x] Azure blob integration
- [x] Merge PDFs
- [x] REST APIs
- [x] Unit Tests
- [x] README
- [x] Postman Collection

---

## 📬 Contact
Created by **Mohit** — [LinkedIn](https://www.linkedin.com/in/mohitkalajain/)  
Let me know if you want deployment setup, Dockerfile, or GitHub Actions for CI/CD.
