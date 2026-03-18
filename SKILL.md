---
name: chatgpt-search
description: This skill enables interaction with ChatGPT via the OpenClaw browser. Use it to: (1) Open ChatGPT, (2) Input queries into ChatGPT, (3) Retrieve responses from ChatGPT.
---

# ChatGPT Search

## Overview

This skill provides a streamlined way to interact with ChatGPT in the OpenClaw browser, allowing you to ask questions and get responses directly.

## Capabilities

### 1. Open ChatGPT

- **Description:** Opens a new tab in the OpenClaw browser and navigates to the ChatGPT interface.
- **Trigger:** When the user explicitly asks to "open ChatGPT" or "launch ChatGPT" in the browser.

### 2. Input Queries

- **Description:** Types a specified query into the ChatGPT input field and submits it.
- **Trigger:** When the user asks to "search" or "ask" something using ChatGPT.

### 3. Retrieve Responses

- **Description:** Captures and extracts the response from ChatGPT after a query has been submitted.
- **Trigger:** Automatically follows a query submission to retrieve the answer.

## Resources

### Interaction Guide

This skill guides you to interact with ChatGPT using the `browser` tool. The process involves:

1.  **Opening ChatGPT**: Navigate to the ChatGPT interface.
    *   `default_api.browser(action="open", profile="openclaw", url="https://chat.openai.com/")`
2.  **Inputting a Query**: Type your question into the chat input field.
    *   First, take a snapshot to find the input field's `ref` (e.g., `e33`).
    *   `default_api.browser(action="act", profile="openclaw", targetId=<chatgpt_tab_id>, request={"kind": "type", "ref": <input_field_ref>, "text": "<your_query>"})`
    *   Then, press Enter to submit.
    *   `default_api.browser(action="act", profile="openclaw", targetId=<chatgpt_tab_id>, request={"kind": "press", "key": "Enter"})`
3.  **Retrieving the Response**: Capture the content after ChatGPT has generated its answer.
    *   Wait for a suitable period or for a specific UI element to indicate completion.
    *   `default_api.browser(action="act", profile="openclaw", targetId=<chatgpt_tab_id>, request={"kind": "wait", "timeMs": 10000})` (adjust time as needed)
    *   Take an AI-formatted snapshot to easily parse the response.
    *   `default_api.browser(action="snapshot", profile="openclaw", snapshotFormat="ai", targetId=<chatgpt_tab_id>)`
    *   Parse the snapshot to extract the latest ChatGPT response. Look for the "ChatGPT said:" heading and extract the subsequent text. Refer to previous interaction examples for the structure.
