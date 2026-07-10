## Changes

- Add Service API for **End User** lookup (`GET /end-users/{end_user_id}`)
  - New method on `DifyBaseClient` (available on chat/chatflow/workflow/completion clients): `EndUserResponse getEndUser(String endUserId)`
  - New model: `EndUserResponse` (id, tenant_id, app_id, type, external_user_id, name, is_anonymous, session_id, created_at, updated_at)
  - Use case: when other APIs return `created_by` as an end-user ID, resolve `external_user_id` / `session_id`
- Add Service API for **Human Input Form** (companion to the Human Input events shipped in 1.3.0)
  - `HumanInputFormResponse getHumanInputForm(String formToken)` — `GET /form/human_input/{form_token}`, fetch a paused form definition
  - `void submitHumanInputForm(String formToken, HumanInputFormSubmitRequest request)` — `POST /form/human_input/{form_token}`, submit inputs + selected action + user to resume the workflow
  - Methods live on `DifyBaseClient` so both workflow and chatflow apps can call them
  - New models: `HumanInputFormResponse`, `HumanInputFormSubmitRequest`
- Add Service API for **Workflow Resume Events** stream (`GET /workflow/{workflow_run_id}/events`)
  - New method on `DifyWorkflowClient`: `void streamWorkflowEvents(String workflowRunId, String user, Boolean includeStateSnapshot, Boolean continueOnPause, WorkflowStreamCallback callback)`
  - After submitting a human-input form, use this endpoint to re-subscribe to the resumed workflow's events (SSE)
  - `include_state_snapshot=true` replays a status summary of already-executed nodes; `continue_on_pause=true` keeps the stream open across multiple pauses
- Introduce reusable GET-SSE helper (`executeGetStreamRequest`) for future streaming endpoints

## Installation

```xml
<dependency>
    <groupId>io.github.imfangs</groupId>
    <artifactId>dify-java-client</artifactId>
    <version>1.4.0</version>
</dependency>
```
