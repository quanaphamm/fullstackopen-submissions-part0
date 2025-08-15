# Part 0 — Fundamentals of Web Apps

## 0.1 HTML
Read [MDN HTML tutorial] — no code to submit.

## 0.2 CSS
Read [MDN CSS tutorial] — no code to submit.

## 0.3 HTML Forms
Read [MDN Your first form tutorial] — no code to submit.

---

## 0.4 New Note Diagram (Classic `/notes` flow)
sequenceDiagram
    participant browser
    participant server

    Note right of browser: User types note and clicks "Save"

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note (form data)
    activate server
    server-->>browser: 302 Redirect to /notes
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/notes
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: CSS file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.js
    activate server
    server-->>browser: JavaScript file
    deactivate server

    Note right of browser: JavaScript runs and fetches notes as JSON

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: JSON data (including new note)
    deactivate server

    Note right of browser: Browser executes callback to render updated notes


## 0.5 SPA Initial Load (/spa)
sequenceDiagram
    participant browser
    participant server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa
    activate server
    server-->>browser: HTML document
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/main.css
    activate server
    server-->>browser: CSS file
    deactivate server

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/spa.js
    activate server
    server-->>browser: JavaScript file
    deactivate server

    Note right of browser: JS runs and fetches notes JSON

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: JSON notes
    deactivate server

    Note right of browser: Browser renders notes via DOM without page reload

## 0.6 SPA — Add a New Note
sequenceDiagram
    participant browser
    participant server

    Note right of browser: User types note and submits form

    Note right of browser: JS intercepts submit (e.preventDefault)

    browser->>server: POST https://studies.cs.helsinki.fi/exampleapp/new_note_spa 
    Note right of browser: Content-Type: application/json; body: { content, date }

    activate server
    server-->>browser: 201 Created (no redirect)
    deactivate server

    Note right of browser: Browser updates local notes array and re-renders list (no GET /notes)

