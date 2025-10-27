# Exercise 0.6 – Creating a New Note in the Single-Page App

This sequence diagram shows what happens when a user creates a new note in the single-page app (SPA) version of the notes app. It illustrates the flow of events between the browser executing JavaScript and the server, highlighting how the note is saved and dynamically displayed without reloading the page.

You can try the live SPA app here: [SPA Notes app](https://studies.cs.helsinki.fi/exampleapp/spa)
```mermaid
   sequenceDiagram
    participant browser
    participant server

    Note right of browser: User types a new note in the SPA and clicks Save

    browser->>server: POST /notes with new note data
    activate server
    Note right of server: Server saves the new note
    server-->>browser: Response with saved note
    deactivate server

    Note right of browser: Browser dynamically updates the notes list without reloading the page
