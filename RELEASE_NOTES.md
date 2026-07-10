## Changes

- Add Service API for **batch document download** as ZIP (`POST /datasets/{dataset_id}/documents/download-zip`)
  - New method on `DifyDatasetsClient`: `FilePreviewResponse downloadDocumentsAsZip(String datasetId, DocumentBatchDownloadRequest request)`
  - Up to 100 document IDs per call; returns `application/zip` binary stream (InputStream + metadata)
  - New model: `DocumentBatchDownloadRequest`
- Add Service API for **single document signed download URL** (`GET /datasets/{dataset_id}/documents/{document_id}/download`)
  - New method on `DifyDatasetsClient`: `DocumentDownloadUrlResponse getDocumentDownloadUrl(String datasetId, String documentId)`
  - Returns a short-lived signed URL for the original uploaded file
  - New model: `DocumentDownloadUrlResponse`
- Add support for the **`reasoning_chunk`** streaming event (Chatflow apps with LLM node `reasoning_format=separated`)
  - New enum: `EventType.REASONING_CHUNK`
  - New event model: `ReasoningChunkEvent` (with nested `data`: message_id, reasoning, node_id, is_final)
  - New callback hook on `ChatflowStreamCallback` and `WorkflowStreamCallback`: `onReasoningChunk`
  - Enables rendering the model's chain-of-thought stream in parallel with the answer, without mixing `<think>` into the message body

## Installation

```xml
<dependency>
    <groupId>io.github.imfangs</groupId>
    <artifactId>dify-java-client</artifactId>
    <version>1.5.0</version>
</dependency>
```
