# Exercise 0.4
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
