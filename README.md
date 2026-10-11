# SkillLoop

A campus skill exchange for students. Instead of paying for tutoring, you trade what you know for what you want to learn.

> I teach you Java, you teach me UI/UX.

Students list the skills they can teach and the skills they want. SkillLoop finds people who fit, including three-person **exchange loops** when nobody matches you directly.

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

## Tech stack

Plain HTML, CSS and JavaScript. No framework, no build step, no server.

## Folder structure

```
skillloop/
  index.html   page layout: login screen and the app shell
  style.css    all styling; colours are variables at the top
  app.js       sample data, matching logic, screens and button actions
  README.md
```

## Running it

1. Download or clone the repository.
2. Open `index.html` in a browser.

**Demo login:** any email and password signs you in as Mohit. Choose "Create an account" to start with an empty profile and 3 credits.

## Things to know

- All data (users, requests, sessions) is stored in memory in `app.js`. Refreshing the page resets everything back to the sample data.
- Login is a demo and does not check passwords.
- Completing a session takes one click. A fuller version would need both students to confirm.

## How matching works

**Direct match.** Two students match when both conditions hold:

- the other student wants at least one skill you offer, and
- the other student offers at least one skill you want.

**Exchange loop.** You teach someone (B), B teaches someone else (C), and C teaches you. In graph terms, each student is a node, each "can teach" link is an edge, and a loop is a cycle of length 3.

Both are in `findMatches()` and `findLoops()` in `app.js`.

## Ideas for later

- Save data on a server so it survives a refresh.
- Real login with passwords.
- Require both students to confirm a completed session.
- Exchange loops longer than three people.
- A session history page.

## Author

Built by Mohit.