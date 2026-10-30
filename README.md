# Workshop 1 - Instructions and knowledge

> 🎯 **Question of the day: what does the chatbot read before it answers?**
>
> A 2-hour workshop, in pairs. You test a model alone, then five chatbots built on the **same
> model** with different instructions, then you write the instructions of **your own** chatbot.
> You leave with your system prompt (`AGENTS.md`), your own test question (question 12), and two
> columns of scores: **Bare** and **A**.

> 🎓 **Open your Codespace** (one per pair): 👉 **https://codespaces.new/Youth-AI-Lab/yal-workshop-preprompt**
>
> This is **workshop 1** of the series "Customising a chatbot". The setup, the commands and the
> common problems: [SETUP.md](SETUP.md). The short version of this page: [sheet.md](sheet.md). The
> whole series: the [workshop kit](https://github.com/Youth-AI-Lab/yal-workshop-kit).

### Contents

- [Goals](#goals)
- [Overview](#overview)
- [Part 1 - Welcome (20 min)](#part-1---welcome-20-min)
- [Part 2 - The test set and the model alone (20 min)](#part-2---the-test-set-and-the-model-alone-20-min)
- [Part 3 - Five personalities (35 min)](#part-3---five-personalities-35-min)
- [Part 4 - Your own system prompt (25 min)](#part-4---your-own-system-prompt-25-min)
- [Part 5 - Closing (10 min)](#part-5---closing-10-min)
- [Troubleshooting](#troubleshooting)

---

## Goals

By the end of this workshop, you will be able to:

- **explain** what the **context** of a model is: everything it reads before it answers;
- **test** a chatbot with a fixed set of questions, and **score** each answer from 0 to 2;
- **explain** why a **system prompt** changes how a chatbot behaves, but not what it knows;
- **tell apart** an honest "I don't know", a confident lie and a reasoning that only looks
  right;
- **write** the system prompt of your own chatbot, with the sections of WikiYouthBot.

**Why it matters for your work with young people.** In the WikiYouthBot activity, the
*Instructions* box of the chatbot is the system prompt of today. You can already build such a
chatbot for a group with Open WebUI: see the [Open WebUI guide](https://github.com/Youth-AI-Lab/yal-openwebui-guide). What young people write in it changes the
tone of the chatbot, its refusals and its honesty. It does not give it knowledge. Today, you see
both, with numbers.

---

## Overview

| Time | Part | What you do | Mode |
|---|---|---|---|
| 20 min | 1. Welcome | open your Codespace, save your key, start Open WebUI in the background | - |
| 20 min | 2. The test set | read the 11 questions, replay them with the model alone, score them by hand; write question 12 | `bare` |
| 35 min | 3. Five personalities | replay the questions with one demo personality, score blind, compare with the judge and the room | `A` |
| 25 min | 4. Your system prompt | write `AGENTS.md`, replay, score blind | `A` |
| 10 min | 5. Closing | your chatbot in Open WebUI, save your work, exit card | - |

10 minutes are left as a margin. The facilitator keeps time.

What enters the context today:

| Mode | What the model reads before your question | Who decides |
|---|---|---|
| `bare` | nothing but the general instructions of the tool | nobody |
| `A` | your system prompt, `AGENTS.md`, in full, at every message | you |

No document enters the context today. Documents come in workshop 2.

---

## Part 1 - Welcome (20 min)

### 📖 One Codespace per pair, one key per pair

You work in a **GitHub Codespace**: VS Code in your browser, with everything installed. The
facilitator gives each pair an **API key**: a long password that lets your Codespace use the
model. Each key has a spending limit.

> ℹ️ **Note.** Each workshop of the series starts in a **new Codespace**. Your work of today is
> kept in a `.zip` file that you download at the end (Part 5), and that you bring back next time.

### Step 1 - Open your Codespace and save your key

1. **Do the [Setup](SETUP.md#setup)**, steps 1 to 5: open your Codespace, let it wait for
   you, save your key with `workshop-login`, have a first conversation, and open a second
   terminal. It takes about 5 minutes.
2. **Check** that you saw this line when you saved your key:

   ```
   Key OK (Claude Code, Anthropic, model claude-sonnet-5-5). You can start: workshop bare
   ```

> 💡 **If you use OpenCode.** OpenCode is another program that runs the same chatbot: same
> modes, same `replay`, same files. Save your key with `workshop-login --engine opencode`
> instead. The differences are in the
> [OpenCode guide, Part 2](https://github.com/Youth-AI-Lab/yal-opencode-guide#part-2---what-opencode-does-compared-with-claude-code).
> The judge of `score` needs an Anthropic key (`sk-ant-`): with an OpenRouter key, you score
> alone.

> ℹ️ **No Codespace?** The same kit opens on your own computer, with Docker and VS Code: see the
> [dev containers guide](https://github.com/Youth-AI-Lab/yal-devcontainer-guide).

### Step 2 - Get ready for workshop 1

1. **In your first terminal**, type:

   ```bash
   workshop-start 1
   ```

   You should see, at the end:

   ```
   Ready for workshop 1.
   Today's page: README.md (Ctrl+Shift+V to read it as a page)
   First command: replay bare
   ```

   This page opens in the editor. Keep it open next to the terminal.

### Step 3 - Start Open WebUI in the background

You will need **Open WebUI**, another chat tool, at the end of the workshop. Its first start takes
a few minutes: start it now.

1. **In your second terminal**, type:

   ```bash
   openwebui start
   ```

2. **Do not wait for it.** Go on with Part 2 in your first terminal. The first time, Open WebUI
   is downloaded (about 4.6 GB): it took 3 min 21 in a Codespace we measured. You should see at
   the end:

   ```
   Open WebUI is ready, with the model "Wildfire RAG (workshop kit)".
   Open it: https://…-3000.app.github.dev
   ```

> 🚫 **Warning.** **Never make port 3000 public** (Ports tab, Port Visibility). This Open WebUI has
> **no accounts**: anyone with the link could use your key. To share a chatbot with a group, see
> the [Open WebUI guide](https://github.com/Youth-AI-Lab/yal-openwebui-guide).

> 💡 **Tip.** **Checkpoint**: `Key OK`, `Ready for workshop 1`, and `openwebui start` running in
> the second terminal.

---

## Part 2 - The test set and the model alone (20 min)

### 📖 Before changing a chatbot, measure it

A model alone has read a lot of text during its training, long ago. It has **no document** of
yours, and it does not know today's date or today's fire danger. Yet it often answers anyway.
Your first job is to see **how often it is right, how often it says "I don't know", and how
often it invents**.

**Why the same questions all series long?** Without a fixed test, you only have impressions. A
chatbot can sound better and be wrong more often. With the same questions and the same
scoring, your columns can be compared. This is the "Press Conference" of WikiYouthBot.

**What is provided**:

- `test-questions.md`: **11 questions, ready to use**, with their expected answer and its source,
  the scoring rules, and an empty question 12 for your territory.
- `scores.md`: your **score sheet**, one short line per question, one column per mode.
- `replay`: the command that asks each question in a **new conversation**, so that nothing
  carries over from one question to the next.

### Step 1 - Read the test set

1. **Open** `test-questions.md` in the file list on the left, then press `Ctrl+Shift+V`
   (`Cmd+Shift+V` on a Mac) to read it as a page.
2. **Read** the scoring rules, then the 11 questions. Notice the **categories**: precise facts,
   explanations, something nobody knows (7), today's level (8), two traps (9 and 10), and a
   document that is not in the kit yet (11).

| Score | When |
|---|---|
| **2** | Right, **and** it says where it comes from. For questions 7 and 9, the right answer is to say so. |
| **1** | Honest but not enough: "I don't know" although the answer exists, or right without its source, or only partly right. |
| **0** | Wrong or invented. **An invented answer is worse than "I don't know".** |

### Step 2 - Predict

Before you replay, **write down in your pair**, on paper: how many questions will the model alone
get right (2)? Which ones? You check it in Step 4.

### Step 3 - Replay the questions with the model alone

1. **In your first terminal**, type:

   ```bash
   replay bare
   ```

   You should see one line per question, then the answer file and the cost:

   ```
   Question 1 (1/11)…
   …
   Question 11 (11/11)…
   Answers: answers/bare-14h05.md   (cost: $…, time: … min … s)
   ```

   It takes about 2 minutes. We measured about $0.10.

2. **While it runs**, open the folder `answers/`: the file is written as the answers arrive.
   Press `Ctrl+Shift+V` to read it as a page.

### Step 4 - Score column Bare, by hand

Today you score the model alone **by hand**: this is how you learn the rules.

1. **Compare** each answer with the expected answer in `test-questions.md`.
2. **Agree** on 0, 1 or 2 in your pair.
3. **Open** `scores.md` and **type the score** in the column **Bare**, between two `|`. For
   example, a score of 1 for question 1:

   ```
   |  1 | EU 2025: hectares and fires       |  1   |      |      |      |      |      |
   ```

4. **Add up** the column in the row **Total**, and **save** (`Ctrl+S`).
5. **Compare** with your prediction of Step 2.

> 💡 **Tip.** **Look for invented details.** The model alone may give a precise figure, the name
> of an organisation or a website, with great confidence. If it is not in the expected answer,
> it gets 0.

### Step 5 - Write question 12, about your territory

Question 12 is **yours**: a precise fact about forest fires where you work with young people.
In workshop 3, you will add its source to the documents of your chatbot.

1. **Read** the section "Question 12: your territory" of `test-questions.md`.
2. **Find one official page** of your territory, and **one precise fact** in it that is not in
   `summaries/`.
3. **Write** the question and its expected answer, with the address of the page, in row 12 of
   `test-questions.md`. Save.
4. **Replay** it with the model alone, then score it in column **Bare** of `scores.md`:

   ```bash
   replay bare 12
   ```

> ℹ️ **Note.** 5 minutes are planned for question 12. If you have not found your page, write the
> question at home, before workshop 2, and replay it then.

### Think about it

The model alone answered some questions without any document. **Where did these answers come
from, and why can it not give a source?** (Hint: when was the model trained?)

> **You built** a test set and a first column. **Reused in** every workshop of the series, and in
> the "Press Conference" of WikiYouthBot.

---

## Part 3 - Five personalities (35 min)

### 📖 Same model, other instructions

A **system prompt** is a text that the model reads **at the start of every conversation**,
before your first message: who the chatbot is, what it is for, which rules it follows. In this
kit, the system prompt is the file `AGENTS.md`. Mode `A` is the model **plus** its system prompt.

The folder `examples/` holds **five system prompts**, for the same model:

| Chatbot | File |
|---|---|
| Feurisson, a hedgehog (inspired by the chatbot of the young people of La Rochelle) | `examples/AGENTS.feurisson.md` |
| Captain Certain | `examples/AGENTS.liar.md` |
| Grandpa Beaver | `examples/AGENTS.storyteller.md` |
| Doctor Proof | `examples/AGENTS.sophist.md` |
| Prudence, an owl | `examples/AGENTS.overcautious.md` |

Three of them make **deliberate errors**. Each of their answers starts with this label:
`⚠️ Demo bot: this answer contains deliberate errors.` Your job is to find **which errors**, and
**how they are made**. This is "I Heard a Rumor" in WikiYouthBot, seen from inside the chatbot.

> ⚠️ **Important.** **Do not open your file before you have scored.** Its name says a lot, its
> content says everything. You open it at Step 4.

### Step 1 - Get your personality

The facilitator gives each pair **one** personality. Write its name here: `________`.

### Step 2 - Replay the questions with it

1. **In your first terminal**, type the command with **your** file, for example:

   ```bash
   replay A --agents examples/AGENTS.liar.md
   ```

   Your `AGENTS.md` is not changed: `--agents` only borrows the other file for this replay. You
   should see, at the end:

   ```
   Answers: answers/A-liar-14h32.md   (cost: $…, time: … min … s)
   ```

   We measured from 1 to 2 and a half minutes, and from $0.03 to $0.17, depending on the
   personality (the storyteller and the sophist write long answers).

### Step 3 - Score blind, then see the judge

`score` shows you each answer next to its expected answer. You type **your** score first. Then a
**judge** shows its score: another model, smaller than the chatbot's, with the same rules as you.

1. **Type** (with the name of **your** answer file):

   ```bash
   score answers/A-liar-14h32.md --blind
   ```

2. **For each question**: read, agree in your pair, type `0`, `1` or `2`, then press Enter. The
   judge's score appears. When you disagree, you see `Disagreement: talk about it.`
3. **At the end**, you see a summary like:

   ```
   You: 4 out of 22 (11 question(s) scored)
   Judge: 2 out of 22 (11 question(s) scored)
   Disagreements: 3
   ```

   Your scores and the judge's go into `scores-personas.md`, not into `scores.md`.

> ℹ️ **Note.** The judge is a model too. It can be wrong. When you disagree, **you** decide, and
> you say why. The judge costs very little: about $0.002 for 11 answers, as we measured.

### Step 4 - Find the trick

1. **Now open** your file in `examples/`. Read the **Identity** and the **Rules**.
2. **Find two answers** where you can show the trick: an invented name, a figure from another
   year or another territory, a fact lost in a story, a refusal although the answer exists.
3. **Write on the board** of the room: your personality, your total, the judge's total, and the
   trick in one sentence.

### Step 5 - Compare in the room

The facilitator shows the table of the room. Discuss:

- **Two chatbots have the same total.** Which ones? Are they the same chatbot?
- **Which errors did you miss, and the judge did not?** Or the reverse?
- **Which one would you give to a group of 14-year-olds?** Why?

> 💡 **Tip.** The errors of these demo bots always make a rule **stricter**, never looser: a lie
> about a ban says that more is forbidden, never less. This is on purpose, for safety.

### Think about it

Feurisson has **no document** in mode A. **How can it score as much as a bot that refuses
everything?** What does a total not show? (Hint: read the answers of Feurisson and Prudence to
question 1. Why does each one refuse? What will each one do when it has documents?)

> **You built** your eye for wrong answers. **Reused in** "I Heard a Rumor" and the "Press
> Conference" of WikiYouthBot, and each time you test a chatbot before you give it to a group.

---

## Part 4 - Your own system prompt (25 min)

### 📖 Instructions change how it behaves, not what it knows

`AGENTS.md` is **your** system prompt. It is read **in full, at every message**. You decide what
is in it, once. Its sections are **the same as in the WikiYouthBot minimal prompt**: Identity,
Theme, Rules, Quality requirements, Target personas, Reference Q&A, Bans and constraints. What you
write here is what young people will write in the *Instructions* box.

**What is provided**:

- `AGENTS.md`: **to complete**. Each section has a hint between `<!--` and `-->`. These hints are
  comments: **they are not sent to the model**.
- `examples/AGENTS.feurisson.md`: a complete example.
- `CLAUDE.md`: *do not modify*. Claude Code reads only this file, and its one line,
  `@AGENTS.md`, imports your system prompt.

### Step 1 - Write it

1. **Open** `AGENTS.md`, then **open the example next to it**: right-click on
   `examples/AGENTS.feurisson.md`, then **"Open to the Side"**.
2. **Write your own** system prompt, under each section title. Take what you like from the
   example, and from the personalities of Part 3. Make it yours: your territory, your
   audience, your tone. **Keep the titles as they are.**
3. **Do not skip Rules and Quality requirements**: the next workshops are scored on them. What
   does it answer when it does not know? When two sources disagree? Does it say where each fact
   comes from?
4. **Save** (`Ctrl+S`).

### Step 2 - Talk to it

1. **Type**:

   ```bash
   workshop A
   ```

2. **Say hello** (`Hello`, then Enter), and look at the **gauge** above the input box. Compare it
   with the same `Hello` in mode `bare`: the difference is the size of your system prompt, read
   again at every message.
3. **Test the behaviour**:
   - `Who are you?`
   - `What is the best insurance company for my house?` (question 9)
   - `How many hectares burnt in Campania in 2025?` (question 7)
4. **Leave**: press **Ctrl+C twice**. If a rule is not followed, change `AGENTS.md`, save, and try
   again.

### Step 3 - Predict, replay, score

1. **Predict** in your pair: which questions will go up from column Bare to column A? Which
   ones will not move?
2. **Replay** in your first terminal:

   ```bash
   replay A
   ```

3. **Score blind** (`score` finds the latest answers of mode A):

   ```bash
   score A --blind
   ```

   This time, your scores go into column **A** of `scores.md`, and the judge's into
   `scores-judge.md`.

4. **Compare** columns Bare and A.

> 💡 **Tip.** **Checkpoint**: `AGENTS.md` has a text under each title, `workshop A` answers with
> your chatbot's identity, and column A is scored.

### Think about it

Even with a perfect system prompt, **why do the precise questions (1 to 4) not improve?** (Hint:
what is in `AGENTS.md`, and what is not?)

> **You built** a system prompt. **Reused in** the *Instructions* box of WikiYouthBot; in the
> system prompt of an Open WebUI chatbot
> ([Open WebUI guide, Step 2 - Write the instructions](https://github.com/Youth-AI-Lab/yal-openwebui-guide#step-2---write-the-instructions));
> in the `AGENTS.md` of an OpenCode chatbot
> ([OpenCode guide, Part 3](https://github.com/Youth-AI-Lab/yal-opencode-guide#part-3---the-instructions-agentsmd)).

---

## Part 5 - Closing (10 min)

### Step 1 - Your chatbot in another tool

Your system prompt is not tied to this tool. In Open WebUI, it becomes the instructions of a
chatbot.

1. **In your second terminal**, check that Open WebUI is ready (Part 1, Step 3), then type, with
   the name of your chatbot:

   ```bash
   openwebui chatbot --name "Feurisson"
   ```

   It takes about 1 minute. You should see at the end:

   ```
   Ready. In Open WebUI (https://…-3000.app.github.dev): New Chat, then choose "Feurisson chatbot" in the message box (bottom right).
   ```

2. **Open the address** (`Ctrl` + click). Choose your chatbot, and ask: `Who are you?`
3. **Ask question 7 and question 1** of the test set. Compare with your answers in mode A.

> ℹ️ **Note.** Your system prompt **travels**: the same text gives the same behaviour in another
> tool. Its **knowledge** does not exist yet: this repository has no documents, so in Open WebUI
> too, your chatbot has nothing to answer question 1 with. Giving it knowledge, and choosing who
> picks the pieces it reads, is the topic of workshops 2 and 3.

### Step 2 - Save your work

1. **Type**:

   ```bash
   workshop-save
   ```

   You should see `Saved … files in my-work.zip:`, then the list of your files.

2. **Download it**: right-click on `my-work.zip` in the file list, then **"Download"**. Bring it
   to workshop 2: in the new Codespace, drag it into the file list, then
   `workshop-start 2 --from my-work.zip` puts your work back.

### Step 3 - Exit card

Answer on the card of the facilitator, alone, in a few words:

1. What does the model read before it answers, in mode A?
2. Name one thing a system prompt changed today, and one thing it could not change.
3. Two chatbots have the same total. What else do you look at before you choose one?

> **To go further.** Run a chatbot on a computer of your organisation, so that nothing leaves it:
> the [local AI guide](https://github.com/Youth-AI-Lab/yal-local-ai-guide). Compare the costs of
> other models and keys: the
> [OpenCode guide, five ways to pay for the model](https://github.com/Youth-AI-Lab/yal-opencode-guide#before-you-start-five-ways-to-pay-for-the-model).

---

## Troubleshooting

The common problems (key, Codespace, terminal) are in the
[Troubleshooting of SETUP.md](SETUP.md#troubleshooting).

**`Instructions file not found: …`** (from `replay --agents`) - Check the name: `examples/`,
then `AGENTS.`, then the personality, then `.md`. Example: `examples/AGENTS.sophist.md`.

**`score` asks for a file.** - Give the name of the answer file of your personality, as `replay`
wrote it: `score answers/A-sophist-14h32.md --blind`. For your own chatbot: `score A --blind`.

**`No judge with an OpenRouter key`** - The judge needs an Anthropic key. Score alone: type your
score for each answer, as in Part 2.

**Question 12 does not appear in `replay`.** - Its question cell is empty, or a `|` is missing.
Compare row 12 with row 11 of `test-questions.md`.

**`openwebui chatbot` says `Warning: your AGENTS.md is still empty`.** - Fill in `AGENTS.md`
(Part 4), save, and type the command again.

**`Open WebUI is not running, or not ready yet.`** - Wait for the line `Open WebUI is ready` in
the second terminal. If the Codespace stopped, type `openwebui start` again.

---

*Youth AI Lab (Erasmus+) - Workshop 1 of the series "Customising a chatbot" - 2026*
