Career Discovery Quiz — for school students from Class 4 to 10.

A short, friendly quiz that helps a Class 4 to 10 (age ~10–16) student explore possible career directions. It asks 27 questions about interests, personality, and how they picture their future, then matches them to 5 careers worth exploring out of 23 possible options — each with its own detailed profile page.

What's in this project
File	What it is	How to use it
index.html	A fully self-contained, offline app	Double-click to open in any browser. No install, no internet needed.

Both files contain the same quiz, scoring logic, and careers — they're kept in sync. The .html file is the one to hand to a student or share directly; the .jsx file is for developers who want to embed the quiz in a larger React app.

Features
27 questions across 5 short sections (Getting to know you → What excites you → How your mind works → The life you imagine → What matters most)
23 career options, spanning medicine, engineering, tech, pure science, education, law, business, arts & design, writing, architecture, sports, culinary, defense/civil services, media, environment, psychology, veterinary science, aviation, music, fashion, and finance
5 results per quiz: the top 4 matches plus one "wildcard" pick worth considering
A full detail page per career — what the job actually involves, a day in the life, school subjects that matter now, skills to build, a realistic path forward through the Indian education system (streams, entrance exams, degrees), and a fun fact
Back navigation — students can revisit and change any earlier answer, including multi-select and ranking questions, without losing their place
Downloadable PDF report — one click generates a printable report with every question answered and all 5 career profiles in full (via the browser's own print-to-PDF)
Sound effects — small, pleasant tones for selecting answers, confirming, finishing a section, and revealing results, generated live with the Web Audio API (no audio files to load — works fully offline). A mute button sits in the top-right corner.
Quiz structure

Each question lives in a QUESTIONS array and has one of three types:

single — pick exactly one option (radio-style)
multi — pick up to max options (checkbox-style, e.g. "pick up to 2")
rank — choose and order your top max priorities (used once, for values)

Every option carries a scores object mapping career keys to points, e.g.:

js
{ label: "Playing sports", scores: { athlete: 3 } }

When the quiz ends, points are summed across every answer (rank questions weight 1st choice highest, 2nd next, 3rd least), and the 5 highest-scoring careers become the result.

A few options also carry an anti list — careers the option actively argues against (used sparingly, e.g. "hating repetitive tasks" nudges away from certain roles).

The 23 careers

Doctor · Engineer · Software Developer / Game Designer · Scientist / Researcher · Teacher / Educator · Lawyer / Judge · Entrepreneur / Business Owner · Artist / Graphic Designer · Writer / Journalist · Architect · Sports Professional / Athlete · Chef / Culinary Professional · Armed Forces / Civil Services Officer · Filmmaker / Content Creator · Wildlife & Environment Scientist · Psychologist / Counselor · Veterinarian · Pilot / Aviation Professional · Musician / Performing Artist · Fashion Designer · Sports Coach / Sports Management · Finance Professional (CA / Analyst / Banker) · Professor / Academic Researcher

Each one is defined as an object with: title, emoji, desc, daylife, subjects, skills, grow, path, and funfact.

Customizing

To add a new career:

Add a new entry to the ROLES object with all 9 fields (title, emoji, desc, daylife, subjects, skills, grow, path, funfact).
Add its key to at least a few existing questions' scores objects (or write a new dedicated question) so it can actually be matched.
In the .html file, ROLES lives near the top of the <script> block. In the .jsx file, it's the first thing in the file.

To add or edit a question:

Add an object to the QUESTIONS array with a unique id, a section (0–4), a type, text, and an options array. Keep ids stable — a few (curiosity_topics, word_pair, gut_check, shadow) are also used to generate the "Why this fits you" reasons shown on results, so renaming them requires updating that logic too.

To rebalance scoring: adjust the point values inside each option's scores object. Higher points = stronger signal toward that career for that answer.

Technical notes
career-discovery-quiz.html — plain HTML/CSS/JavaScript, no frameworks, no CDN dependencies, no build step. Rendering uses simple template strings and one delegated click handler; state lives in a single JS object. This is intentional: it means the file works forever, offline, on any device, with nothing to install or go stale.
career-discovery-quiz.jsx — a React functional component using useState and useMemo, written for environments that already have React set up (e.g. a Claude.ai artifact or an existing React app). It includes the same questions, careers, back navigation, and printable PDF report as the HTML version. The one thing it doesn't include is sound effects — those were built specifically for the standalone HTML file and haven't been ported back into the React component.
The PDF report uses the browser's native print dialog (window.print()) rather than a PDF-generation library, so it needs no external dependencies either.
