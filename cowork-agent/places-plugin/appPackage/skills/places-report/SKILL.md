---
name: places-report
description: Generate a markdown report of recommended places to visit near the user's location by asking the "Places To Visit" Copilot Studio agent, with a trace of the agent interaction appended. Use when the user asks for places to visit, things to see, or a places report near them or a named location.
---

# Places Report

Produce a markdown file containing a table of places to visit near the user's
location, sourced from the **Places To Visit** Copilot Studio agent (exposed via
the `Places To Visit` agent connector), followed by trace details of the
interaction with that agent.

## When to use this skill

- The user asks "what places can I visit near me?", "places to go around <location>",
  "create a places report", or similar.
- The user wants recommendations for places to visit written up as a markdown table/report.

## Inputs

- **Location** (required): Use the location the user states. If none is given, use the
  user's known location from their profile/context (e.g. office city). If no location
  can be determined, ask the user for one before calling the agent. Never invent a location.
- **Optional filters**: category (e.g. museums, parks, food), distance/radius, number of
  results. Default to up to 10 places if the user does not specify.

## How to do it

1. **Resolve the location** as described above and record the exact value used.
2. **Call the Places To Visit agent** using the tool(s) provided by the `Places To Visit`
   connector. Send a clear natural-language request, for example:
   `List up to 10 recommended places to visit near <location>. For each place give the name,
   category/type, approximate distance from <location>, a short description, and why it is worth visiting.`
   Include any user filters in the request.
   - Record for the trace: tool name, the exact request sent, the UTC start timestamp,
     the UTC end timestamp, any conversation/correlation IDs returned, and the outcome.
   - If the agent asks a clarifying question, answer it from the user's inputs if possible,
     otherwise relay it to the user, then call the agent again. Record every call.
3. **Build the table only from the agent's response.** Do not add, embellish, or reorder
   facts with your own knowledge. If a field is not provided by the agent, write `—`.
4. **Write the markdown file** named `places-report-<location-slug>-<YYYY-MM-DD>.md`
   using exactly this structure:

   ```markdown
   # Places to Visit near <Location>

   _Generated <YYYY-MM-DD HH:mm UTC> from the Places To Visit agent._

   | # | Place | Type | Distance | Description | Why visit |
   |---|-------|------|----------|-------------|-----------|
   | 1 | ...   | ...  | ...      | ...         | ...       |

   ---

   ## Trace details

   | Field | Value |
   |-------|-------|
   | Agent | Places To Visit (Copilot Studio) |
   | Connector | Places To Visit (remote MCP) |
   | Tool(s) invoked | <tool name(s)> |
   | Location used | <location> (<source: user-provided / profile>) |
   | Request sent | <exact prompt sent to the agent> |
   | Started (UTC) | <timestamp> |
   | Completed (UTC) | <timestamp> |
   | Duration | <ms or s> |
   | Number of calls | <n> |
   | Conversation / correlation ID | <id or "not returned"> |
   | Places returned | <count> |
   | Status | Success / Partial / Failed (<reason>) |

   ### Raw agent response

   <details><summary>Show response</summary>

   <verbatim agent response text>

   </details>
   ```

   If more than one call was made, add one row per call (or a numbered sub-section) in the
   trace so every interaction is visible.
5. Return the file to the user and give a one-line summary (location and number of places).

## What to watch for

- **Authentication**: The connector uses OAuth. If the call fails because the user is not
  signed in or consent is required, tell the user to sign in to the connector and retry. Still
  produce the trace section with `Status: Failed` and the error message.
- **Empty or off-topic responses**: If the agent returns no places, write the table header
  with a single row stating "No places returned by the agent" and keep the trace.
- **Do not fabricate** places, distances, or IDs. Unknown values are `—` or "not returned".
- Never include tokens, secrets, or authorization headers in the trace.
- Out of scope: booking, directions, or itinerary planning — suggest the user ask separately.
