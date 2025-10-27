# Exercise 0.4 – Creating a New Note

This sequence diagram shows what happens when a user creates a new note on the notes page. 
It illustrates the flow of events between the user, the browser executing JavaScript, and the server saving the note and responding back.

You can try the live app here: [Notes app](https://studies.cs.helsinki.fi/exampleapp/notes)

```mermaid
sequenceDiagram
    participant User
    participant Browser
    participant Server

    Note right of User: User types a new note into the text field
    User->>Browser: Click Save button
    Note right of Browser: Browser executes JS function to handle save
    Browser->>Server: POST /notes with new note data
    activate Server
    Note right of Server: Server receives request, saves note to data.json
    Server-->>Browser: Response with saved note
    deactivate Server
    Note right of Browser: Browser executes callback, updates the page
    Browser-->>User: New note displayed on the page
