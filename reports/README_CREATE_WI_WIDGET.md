Create Work Item widget for Polarion reports

This repository now contains a Velocity template `workItemCreation.vm` which renders
an HTML form and supports both client-side (REST) and server-side creation of
work items.

Server-side creation notes
- The template attempts server-side creation when you submit the form with the
  "Create (server-side)" button. It tries several common patterns in Polarion
  Velocity contexts:
  1. Use `$workItemService` if present and call `createWorkItem(projectId,type,title)`.
  2. Use `$workitemService` (alternate capitalization) if present.
  3. Use `$componentLocator.getService(...)` to find a WorkItemService under
     likely class names.
- These attempts are best-effort: Polarion deployments expose different service
  names and method signatures. If the server-side attempt fails the template
  will display diagnostic messages to help you adapt it.

How to adapt for your environment
- If you have an example server-side invocation (from an existing Velocity
  report or plugin) that successfully creates a work item in your installation,
  paste it here and I will adapt `workItemCreation.vm` to call the same API.
- Common adjustments:
  - Replace `createWorkItem(...)` with the exact method your service requires.
  - If extra parameters or helper objects are required (session, user,
    field maps), ensure those variables are exposed in the Velocity context
    or obtained via `$componentLocator`.

Testing
- Deploy `workItemCreation.vm` into a Polarion report and view it while logged
  in.
- Use the "Create (server-side)" button; any success or error message will be
  rendered above the form.

If you'd like, I can now:
- Modify the template to call a concrete API if you paste a working example,
  or
- Remove the client-side REST fallback and keep only server-side logic.
