# SkillLoop

A campus skill exchange for students. Instead of paying for tutoring, you trade what you know for what you want to learn.

> I teach you Java, you teach me UI/UX.

SkillLoop is not just a tutoring board. It tracks an exchange economy: students list skills they can teach and skills they want, and the app finds people who fit, including three-person **exchange loops** when nobody matches you directly.

```
Mohit teaches DSA     ->  Dev
Dev teaches Photoshop ->  Meera
Meera teaches Cloud   ->  Mohit
```

## Features

- **Accounts and profiles:** sign up, log in, edit your name and course.
- **Offered and wanted skills:** add or remove skills on your profile.
- **Direct matches:** finds students who want something you offer and offer something you want.
- **Exchange loops:** finds three-person cycles (you to B to C to you).
- **Exchange requests:** send, accept or decline a swap.
- **Session scheduling:** an accepted swap becomes two sessions, each with a date and time.
- **Completion and ratings:** mark a session complete, then rate the teacher from 1 to 5.
- **Skill credits:** the teacher earns 1 credit and the learner spends 1 when a session completes.

## Project status

| Part | State |
| --- | --- |
| Frontend (HTML, CSS, JavaScript) | Done. Runs on its own with sample data. |
| Backend (Java, Spring Boot) | Planned. The frontend is written so it can be connected later. |

The frontend keeps all data in memory, so refreshing the page resets it. The matching code in `app.js` exists only to make the demo work. The real matching engine is meant to live in the Java backend.

## Tech stack

- **Frontend:** plain HTML, CSS and JavaScript. No framework, no build step.
- **Backend (planned):** Java and Spring Boot.

## Folder structure

```
skillloop/
  index.html   page layout: login screen and the app shell
  style.css    all styling; colours are variables at the top
  app.js       sample data, matching logic, screens and button actions
  README.md
```

## Running the frontend

1. Download or clone the repository.
2. Open `index.html` in a browser.

That is all. No install needed.

**Demo login:** any email and password signs you in as Mohit. Choose "Create an account" to start with an empty profile and 3 credits.

To serve it from Spring Boot later, copy the three files into `src/main/resources/static/`.

## How matching works

**Direct match.** Two students match when both conditions hold:

- the other student wants at least one skill you offer, and
- the other student offers at least one skill you want.

**Exchange loop.** A loop exists when you teach someone (B), B teaches someone else (C), and C teaches you. In graph terms, each student is a node, each "can teach" link is an edge, and a loop is a cycle of length 3. The backend can extend this to longer cycles with a graph search.

## Connecting the backend

All data lives at the top of `app.js` (the `users`, `requests` and `sessions` arrays). To connect Spring Boot, replace those arrays with `fetch()` calls. A suggested set of endpoints:

| Method | Endpoint | Purpose |
| --- | --- | --- |
| POST | `/api/auth/register`, `/api/auth/login` | Authentication |
| GET, PUT | `/api/users/me` | View and update your profile and skills |
| GET | `/api/matches` | Direct matches and exchange loops |
| POST | `/api/requests` | Send a swap request |
| PATCH | `/api/requests/{id}` | Accept or decline |
| PATCH | `/api/sessions/{id}` | Schedule, confirm completion, rate |

In the frontend, completing a session takes one click. In the real app, both students should confirm before credits move.

## Roadmap

- Build the Spring Boot backend and database.
- Move matching and loop detection into Java.
- Require both students to confirm a completed session.
- Support exchange loops longer than three people.
- Add a session history page.

## Author

Built by Mohit.