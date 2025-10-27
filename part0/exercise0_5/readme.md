# Exercise 0.5 – Loading the Single-Page App

This sequence diagram shows what happens when a user opens the single-page app (SPA) version of the notes app. It illustrates the flow of events between the browser executing JavaScript and the server, including how the HTML, CSS, JavaScript, and existing notes are fetched and rendered dynamically.

You can try the live SPA app here: [SPA Notes app](https://studies.cs.helsinki.fi/exampleapp/spa)



```mermaid
    sequenceDiagram
    participant browser
    participant server

    Note right of browser: User opens the SPA notes app

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

    Note right of browser: Browser executes JS to fetch and render existing notes

    browser->>server: GET https://studies.cs.helsinki.fi/exampleapp/data.json
    activate server
    server-->>browser: JSON list of existing notes
    deactivate server

    Note right of browser: Browser dynamically renders notes on the page
