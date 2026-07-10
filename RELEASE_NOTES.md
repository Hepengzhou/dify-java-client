## Changes

- Add Human Input (HITL) workflow event support for Dify 1.14.2+ (#162)
  - New events: `human_input_required`, `workflow_paused`, `human_input_form_filled`, `human_input_form_timeout`
  - New event models: `HumanInputRequiredEvent`, `WorkflowPausedEvent`, `HumanInputFormFilledEvent`, `HumanInputFormTimeoutEvent`
  - New callback hooks on `WorkflowStreamCallback` and `ChatflowStreamCallback`: `onHumanInputRequired`, `onWorkflowPaused`, `onHumanInputFormFilled`, `onHumanInputFormTimeout`

