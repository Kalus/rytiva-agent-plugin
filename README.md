# Rytiva

Plan workouts in conversation, send them to Rytiva on iPhone and Apple Watch, and review your recorded training. Useful workout and history cards remain available in compatible clients.

This package is prepared for local validation. Public directory availability is not established by this repository. The internal package name and `repdeck_` tool prefix remain stable for compatibility; the displayed product is Rytiva.

## Connect

The remote MCP endpoint is `https://repdeck-bridge.lukasfauset.workers.dev/mcp` (Streamable HTTP). Use your host's normal OAuth connection flow and sign in with your existing Rytiva account. Do not put credentials in chat, skill files, or MCP headers. The package requires no local server or API key.

Verified identity-provider authority/subject pairs link to a durable Rytiva account. Email equality alone does not merge accounts. TestFlight and App Store app installations use this same service and workout library; there is no separate Beta connector to select.

Reading the library and history uses the connected account. Creating or changing prescriptions and schedules requires Rytiva Pro. A service or entitlement error must not be presented as a successful save.

## Workflows

- [Plan a workout](skills/plan-workout/SKILL.md): create, edit or schedule an exact user-directed plan; preserve exercise choices and retry safely.
- [Review training](skills/review-training/SKILL.md): summarize returned inbox, history and limited training data; suggest next steps without inventing missing measurements.

Direct create, update, schedule and versioned-command tools require `user_confirmed: true` when the current instruction or prior approval covers the final operation. Resolve ambiguity in chat first. No additional app review is required. Only `receipt.status: applied` confirms persistence; the legacy `kind: proposal` label does not change that rule. Device arrival depends on normal sync.

Reuse an unchanged request and its idempotency key after a lost response. Persisted draft/recovery tools are also available, but recording or approving a draft does not mean the workout was saved. Do not create a replacement workout merely to edit an existing ID.

Catalog membership does not guarantee playable video. Resolve references silently and use only exact available `image_key` values returned by the catalog tool. Keep the requested exercise when media is unavailable; never invent keys or send provider URLs/IDs.

## Tools and cards

The server currently exposes 19 tools:

| Capability | Tools (all begin with `repdeck_`) |
| --- | --- |
| Exercise lookup | `find_exercise_reference_media`, `list_exercise_reference_media` |
| Direct plan changes | `create_workout`, `update_workout`, `schedule_workout`, `apply_workout_command` |
| Drafts and recovery | `propose_workout`, `list_workout_proposals`, `get_workout_proposal`, `decide_workout_proposal`, `apply_workout_proposal` |
| Workout library | `list_inbox_workouts`, `get_workout`, `list_trash_workouts`, `delete_workout`, `restore_workout`, `set_workout_favorite` |
| Training review | `list_completed_workouts`, `get_training_summary` |

Inbox, workout, trash, history, summary and library-action tools retain their existing card links. Routine media checks, direct saves and proposal/recovery responses use text and structured data. The host controls tool-call visibility; this package does not promise to hide its activity indicators.

Single-instance changes require real occurrence IDs and a current revision. The current inbox/get tools do not enumerate those IDs, so a client lacking occurrence context must explain that limitation. Whole-plan scheduling replaces both supplied schedule lists; callers must preserve the other list when editing only one.

## Package contents

The root `.mcp.json` supplies the same endpoint to the Codex and Claude manifests. Both use the two shared skill folders. A public OpenAI submission must scan this remote server directly; an existing integration ID is not the submission artifact. Claude's Cowork/Code plugin and its chat connector are distinct distribution paths.

This thin plugin bundle is licensed under the [MIT License](LICENSE), copyright 2026 MossFauset Digital. That license applies to this bundle only; it does not license the separately hosted Rytiva service, iPhone/Watch app, or backend repository. Service access remains subject to its terms and entitlements. Maintainers export an explicit allowlist; app/backend code and local integration configuration are not included.

Initial directory distribution is planned for the United States. Directory review and live connection testing remain pending; a public source repository is not directory approval.

## Privacy and support

Rytiva processes authored plans, completion history, set notes and limited workout/heart-rate summaries, not your complete HealthKit history. Authorizing an assistant makes requested data available to that service. See the [privacy policy](https://repdeck-bridge.lukasfauset.workers.dev/privacy), [terms](https://repdeck-bridge.lukasfauset.workers.dev/terms), [support](https://repdeck-bridge.lukasfauset.workers.dev/support) and [connection documentation](https://repdeck-bridge.lukasfauset.workers.dev/docs/mcp).

Support is available at support@rytiva.com. Never include authentication codes, tokens or passwords in a support report. The plugin homepage is https://rytiva.com/claude-plugin/; directory review and live connection testing remain publication gates.
