# Raahi: Local Public Transport Route Assistant for Agra

Raahi helps people in Agra find city bus routes by simply asking a question in plain language, such as *"bus from Foundry Nagar to Tajmahal after 2 PM"*. It returns the matching route with its stops and next departure times.

**SDG alignment:** SDG 11, Sustainable Cities and Communities (Target 11.2: accessible public transport).

---

## Problem

People in Agra find it hard to know which bus to take and when it leaves. Timetables are scattered across government documents and websites, and many routes share the same stops. Many people therefore choose autos and private vehicles, which adds to traffic and pollution.

## Solution

Raahi is a web app backed by a **RAG (Retrieval-Augmented Generation)** service. The real AMCTSL bus timetable is stored in a vector database. When a user asks a question, the backend retrieves the most relevant routes, and the web app shows them as easy-to-read route cards.

## Features

- **Ask Raahi:** plain-language route search, including time requests like "after 2 PM"
- **Explore routes:** browse all routes and search by stop name
- **Live board:** upcoming departures with a countdown
- **Saved routes:** keep your regular routes in one place
- **Dashboard:** recent searches and backend status
- **Demo login** and profile page

## How it works

```
User question
     |
     v
Web app (HTML / CSS / JavaScript)
     |   GET /ask?query=...
     v
FastAPI backend  -->  ChromaDB (vector search over route data)
     |
     v
{ "retrieved": [ { "id": "R-6", ... } ] }
     |
     v
Web app shows the route card with stops and departure times
```

The backend returns the IDs of the matching routes. The web app holds the full route details and time filtering logic.

## Tech stack

| Layer | Technology |
|---|---|
| Frontend | HTML, CSS, JavaScript, Google Fonts (Space Grotesk, IBM Plex Mono) |
| Backend | Python, FastAPI, Uvicorn |
| Database / AI | ChromaDB (vector database), RAG-based retrieval |
| Data | AMCTSL (Agra-Mathura City Transport Service Ltd.) timetable, published at uputd.gov.in |

## Data

- 14 bus routes (R-1 to R-14)
- 24 different stops
- 98 scheduled departures

## Project structure

```
raahi-transit-assistant/
├── raahi-backend/        # FastAPI + ChromaDB backend (main.py)
├── raahi_web_app.html    # Frontend (single file)
└── README.md
```

## Getting started

### 1. Start the backend

```bash
cd raahi-backend
pip install fastapi uvicorn chromadb
python -m uvicorn main:app --reload
```

The API runs at `http://127.0.0.1:8000`. You can test it in the browser:

```
http://127.0.0.1:8000/ask?query=bus to Tajmahal
```

### 2. Open the frontend

Open `raahi_web_app.html` in your browser. Log in with any email and password (the login is for demo only). The dashboard shows **Online** when the backend is reachable.

> If the frontend cannot reach the backend, make sure the backend is running and that CORS is enabled in FastAPI (`CORSMiddleware`).

## Limitations

- Covers 14 Agra city bus routes only
- Fixed timetable, no live GPS tracking
- Queries in English only
- Demo login: no real accounts, and data is not saved after a page refresh

## Future scope

- Hindi and voice input
- Fare and accessibility information
- Live bus tracking
- More routes, more cities and real user accounts

## Team

- Name: _add your name_
- College: _add your college_
- Guide: _add guide name_
