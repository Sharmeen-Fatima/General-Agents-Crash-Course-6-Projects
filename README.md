# AI Agent Fundamentals — Six-Project Practical Exercise

A hands-on crash course exploring how general-purpose AI agents behave on the web — covering tool execution, state and file tiers, permission gates, cloud scheduling, cross-product comparison, and vendor portability.

**Status:** ✅ All 6 projects completed

---

## Table of Contents

1. [Project 1 — The Worker / Tool-Location Test](#project-1--the-worker--tool-location-test)
2. [Project 2 — The Three-Tier Audit](#project-2--the-three-tier-audit)
3. [Project 3 — The Gate Lab](#project-3--the-gate-lab)
4. [Project 4 — The First Cloud Schedule](#project-4--the-first-cloud-schedule)
5. [Project 5 — One Task, Two Harnesses](#project-5--one-task-two-harnesses)
6. [Project 6 — The Portability Drill](#project-6--the-portability-drill)
7. [Overall Summary](#overall-summary)

---

## Project 1 — The Worker / Tool-Location Test

**Goal:** Understand the difference between where an AI agent *thinks* (agent-loop location) and where a tool actually *runs* (tool-execution location).

### What Was Done
- Started a task in the cloud using only a web-reachable source, then closed and reopened it from another device — the task remained complete.
- Connected a local folder on the desktop app and asked the agent to read a file from it.
- Tested access after moving the file, and again after disconnecting the folder connector, to observe how local access behaves.

### Result / Finding
- Cloud-only tasks do not depend on any single device; the reasoning happens on the server, so closing a tab does not stop the work.
- Local-folder tasks depend on live, real-time access to that folder — if the file moves or access is removed, the task fails or reports the file as missing.

<!-- Add screenshot: ![Project 1 screenshot](./screenshots/project1.png) -->

**Status:** ✅ Complete

---

## Project 2 — The Three-Tier Audit

**Goal:** Trace a real task from where its context lives to where its final output is stored, and identify what would be lost if the account disappeared.

### What Was Done
- Asked the agent to summarize a website into a PDF, in a normal chat session.
- Saved the finished PDF to Google Drive using the Google Drive connector.

### Result / Finding
- **State layer used:** Session (a plain chat, no saved Project or memory involved).
- **Final file tier:** Tier 3 — a real file saved in Google Drive, independent of the vendor account.
- If the account were deleted, the chat history would be lost, but the PDF in Google Drive would remain safe.

<!-- Add screenshot: ![Project 2 screenshot](./screenshots/project2.png) -->

**Status:** ✅ Complete

---

## Project 3 — The Gate Lab

**Goal:** Observe the difference between actions an AI can take automatically and actions that require explicit approval.

### What Was Done
- Asked the agent to draft (not send) a meeting-reminder email through the Gmail connector.
- Asked the agent to then send that draft, to see if approval was requested.

### Result / Finding
- **Allowed automatically:** creating the email draft — no approval was requested.
- **Escalated for approval:** sending the email — the agent asked for confirmation through Gmail before sending.
- **Chosen approach for real workflows:** let the AI draft freely, but always review and approve before anything is actually sent, since sending is irreversible.

<!-- Add screenshot: ![Project 3 screenshot](./screenshots/project3.png) -->

**Status:** ✅ Complete

---

## Project 4 — The First Cloud Schedule

**Goal:** Build a recurring cloud task that runs on its own schedule, independent of any device being on.

### Six Answers Defined Before Scheduling
| Question | Answer |
|---|---|
| **Trigger** | A fixed time each day, plus a fixed day and time each week |
| **Touch** | Web search plus the Gmail and Google Drive connectors — all cloud-reachable, no local folder used |
| **Device independence** | The task must run whether or not the computer is on |
| **Success signal** | A PDF appears in Google Drive (daily), and an email arrives (weekly) |
| **Autonomy** | Runs fully automatically, with approvals set to always allow for this low-risk task |
| **Empty case** | If there is no major news, the task still produces a short PDF saying so, instead of skipping the run |

### What Was Done
- Built a scheduled task: daily research with the PDF saved to Google Drive, plus a Wednesday email with a consolidated weekly summary.
- Tested the workflow manually before scheduling, then left the computer switched off at the scheduled run time on two separate days.

### Result / Finding
- The task fired successfully on its own, with the computer off, on two separate occasions.
- Each run left a verifiable Tier 3 output — a PDF saved to Google Drive.

<!-- Add screenshot: ![Project 4 screenshot](./screenshots/project4.png) -->

**Status:** ✅ Complete

---

## Project 5 — One Task, Two Harnesses

**Goal:** Give the identical task to two different AI products and compare how each implements the same underlying structure.

### What Was Done
The same prompt was given to both **ChatGPT Work** and **Claude Cowork**: search the web for today's top 3 AI industry news stories, summarize each, save as a PDF, show reasoning, and ask for approval before finalizing.

### Comparison

| Concept | ChatGPT Work | Claude Cowork |
|---|---|---|
| **Heartbeat** | Started immediately after the prompt was sent. | Started immediately after the prompt was sent (same). |
| **Reach** | Ran a smaller number of broader web searches. | Ran multiple targeted searches per company, plus page fetches for verification. |
| **Loop** | Reasoning steps were mostly hidden; went straight to a request for approval. | Reasoning was shown step by step, including why each story was chosen. |
| **Gate** | Asked for approval, then built and delivered the PDF right away. | Asked for approval and waited; only built the PDF after an explicit "yes." |
| **Body** | Delivered the PDF directly after approval. | Built the PDF using a document skill, visually verified it, then delivered it. |

**Conclusion:** Both products followed the same six-part shape (heartbeat, reach, loop, spine, gate, body), but implemented at least three of those parts differently — most notably how strictly each one honored the approval gate before producing the file.

<!-- Add screenshots: ![ChatGPT Work log](./screenshots/project5-chatgpt.png) ![Claude Cowork log](./screenshots/project5-claude.png) -->

**Status:** ✅ Complete

---

## Project 6 — The Portability Drill

**Goal:** Assume the AI vendor disappears tomorrow. Using only Tier 3 files and personally-owned notes, work out what of a real workflow could still be rebuilt — and what could not.

### Workflow Used For The Drill
The Project 4 daily/weekly tech-news workflow: its instructions, its cloud sources, its definition of done, and its last saved PDF.

### Reconstruction Check

| ✅ Could Be Reconstructed (Tier 3 / Own Notes) | ❌ Could NOT Be Reconstructed (Lock-in Risk) |
|---|---|
| Original prompt text, once saved outside the chat. | Exact scheduled-task configuration (frequency, approval mode setting). |
| Final PDF outputs already saved to Google Drive. | The exact search-and-reasoning process used to research and choose stories. |
| Definition of done, once written down (e.g. "PDF appears in Drive"). | Connector permissions (Gmail, Google Drive) — would need to be reconnected from scratch on another tool. |
| General source description ("web search for tech news"). | Full conversation history and context built up across the chat. |

### Lock-in Exposure (Next Portability Backlog)
- Write down the exact scheduled-task settings (times, approval mode) outside of the product itself.
- Keep a short written definition of done for each recurring task, separate from the chat.
- Expect to fully reconnect any connectors (Gmail, Drive) from scratch on a different AI product.

<!-- Add screenshot: ![Project 6 screenshot](./screenshots/project6.png) -->

**Status:** ✅ Complete

---

## Overall Summary

| Project | Focus | Status |
|---|---|---|
| 1 | Agent-loop location vs. tool-execution location | ✅ Complete |
| 2 | Tracing state layers and file tiers | ✅ Complete |
| 3 | Automatic actions vs. approval gates | ✅ Complete |
| 4 | Building a reliable cloud schedule | ✅ Complete |
| 5 | Comparing two AI products on the same task | ✅ Complete |
| 6 | Planning for vendor independence | ✅ Complete |

---

## Notes

- All exercises used low-stakes, non-regulated data only (tech news, test emails). No banking, medical, identity, or other sensitive data was accessed.
- Screenshots referenced above should be placed in a `screenshots/` folder in this repository, matching the filenames in the commented-out image links.
