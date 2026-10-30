# Workshop 1 - Instructions and knowledge (one page)

**Question of the day: what does the chatbot read before it answers?**
Full page: [README.md](README.md). Setup and common problems: [SETUP.md](SETUP.md).

| Score | When |
|---|---|
| **2** | Right, and it says where it comes from (7 and 9: saying "I don't know" or refusing is right). |
| **1** | Honest but not enough: "I don't know" although the answer exists, no source, or partly right. |
| **0** | Wrong or invented. |

## 1. Welcome (20 min)

1. Open the Codespace: **https://codespaces.new/Youth-AI-Lab/yal-workshop-preprompt** → **Create codespace**.
2. https://github.com/settings/codespaces → **Default idle timeout**: **120** minutes, save.
3. Terminal 1: `workshop-login`, paste the key once, Enter → you see `Key OK`.
4. Terminal 1: `workshop bare`. First time: keep the theme (Enter), **trust the folder**. `Hello`,
   look at the gauge. `Ctrl+C` twice.
5. Terminal 1: `workshop-start 1` → you see `Ready for workshop 1`.
6. Terminal 2 (`+` in the terminal panel): `openwebui start`. Do not wait: go on in terminal 1.
   Terminal 2 ends with `Open WebUI is ready`.

## 2. The test set (20 min)

1. Read `test-questions.md` (`Ctrl+Shift+V`).
2. Predict on paper: how many 2s for the model alone?
3. Terminal 1: `replay bare` → a file in `answers/`.
4. While it runs, terminal 3 (`+`): `workshop bare`, ask question 1, then
   `Where does this figure come from? Give me your source.` Look at the gauge. `Ctrl+C` twice.
5. Score each answer **by hand** in column **Bare** of `scores.md`. Save (`Ctrl+S`).
6. Row 12 of `test-questions.md`: click the file in the file list to write in it (you cannot type
   in the `Ctrl+Shift+V` page). One question about **your territory**, its answer, its source. Save.
   Then `replay bare 12`, and score it.

## 3. Five personalities (35 min)

1. Get one personality from the facilitator. **Do not open its file yet.**
2. `replay A --agents examples/AGENTS.liar.md`, with your personality instead of `liar`.
   At the end you see a line like `Answers: answers/A-liar-14h32.md`.
3. `score answers/A-liar-14h32.md --blind`, with the file name of your `Answers:` line: your
   score first, then the judge's.
4. Open the file in `examples/`: find the trick. Write on the board: name, your total and the
   judge's total (with the "out of" that `score` prints), the trick in one sentence.

## 4. Your system prompt (25 min)

1. Fill in `AGENTS.md` under each title (example: `examples/AGENTS.feurisson.md`). Save.
2. `workshop A`: `Hello`, look at the gauge and compare with bare; `Who are you?`; questions 7
   and 9. `Ctrl+C` twice.
3. Predict: which questions go up from Bare to A?
4. `replay A`, then `score A --blind`. Compare columns Bare and A.

## 5. Closing (10 min)

1. Terminal 2: `openwebui chatbot --name "Feurisson"`, with the name of your chatbot. Open the
   address it prints (`Ctrl` + click, or **Ports** → 3000). **New Chat**, then choose your chatbot
   (its name + `chatbot`) in the message box, bottom right. Ask `Who are you?`, then questions 7
   and 1. Same behaviour as in mode A?
2. `workshop-save` → right-click on `my-work.zip` → **Download**. Bring it to workshop 2.
3. Exit card: three answers, alone.

**Leave a conversation:** `Ctrl+C` twice. **Copy / paste in the terminal:** `Ctrl+Shift+C` /
`Ctrl+Shift+V` (`Cmd+C` / `Cmd+V` on a Mac). **Never make port 3000 public.**
