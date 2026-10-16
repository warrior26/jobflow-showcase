# How I built it

I'm a product manager, not a full-time engineer. I built Jobflow the way I'd run a small product team, except the team was an AI coding agent: Claude Code, working in my repository on my laptop.

## The loop

1. I write the requirement in plain English, with the acceptance rule: what must be true when it's done.
2. The agent reads the code it needs, makes the change, writes tests for it and runs the whole suite.
3. I try it in the running app with real job postings. When it's wrong, I say what I saw and what I expected, and we go around again.
4. When a rule should hold from then on, it goes into a context file the agent reads at the start of every session.

The test suite has 191 tests.

## Some of the requirements, and what they became

### Mark a job Applied when the application goes through

The form filler now reads the page after Submit and marks the job Applied only when the employer's site shows a confirmation. If it can't tell, it leaves the job alone and says to check email.

### Fill the form and let me press Submit

This became hand-off mode. The browser opens, every field it can answer is filled, the resume and cover letter are attached, and the window stays open for me.

### Hide roles with no direct link to apply

Some postings came through boards whose Apply button led to a paid sign-up. Those wasted time, so Jobflow now looks for the same role on the employer's own board and hides the posting when there isn't one.

### Show the number of employees next to each job

Each job now carries an approximate headcount from Wikipedia, the Y Combinator company list or the posting text, with strict name and size checks so one company isn't mistaken for another with a similar name.

### Search career sites near my zip code

The app finds employers near a zip code through OpenStreetMap and Wikidata, works out which career platform each one uses, and reads their open roles.

### Use free connectors only

I wanted no email registration and no monthly plan, so this became a standing rule in a context file. Connectors that needed a sign-up were dropped, and the free Himalayas, Jobicy and Arbeitnow boards were added.

## Context the agent works from

- A master resume with every role, date, result and skill I can claim. Tailoring may select and reorder; it may not change a fact.
- Memory files that carry standing rules between sessions, such as how resume lines must read (past tense, plain English, me as the actor) and the free-connectors rule.
- An agent definition for a separate browser agent that applies in my own Chrome. The markdown file lists its tools, the step-by-step procedure, and the hard stops: CAPTCHAs, verification codes, account sign-ups, and any question it cannot answer truthfully.
