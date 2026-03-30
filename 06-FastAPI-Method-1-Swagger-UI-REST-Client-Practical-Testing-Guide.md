<a id="top"></a>

# Swagger UI — Step-by-Step Testing Guide
## Task Manager API — `main.py`

> **Tool used: Swagger UI only** — nothing else to install.
> This guide tells you exactly where to click, what to type, and what you should see.
> Follow every step in order. Do not skip anything.

---

## Table of Contents

| # | What you will test |
|---|---|
| 0 | [Start the server and open Swagger UI](#s0) |
| 1 | [TEST 1 — GET `/` — Is the server alive?](#s1) |
| 2 | [TEST 2 — GET `/tasks` — List all tasks](#s2) |
| 3 | [TEST 3 — GET `/tasks` with a filter — only completed tasks](#s3) |
| 4 | [TEST 4 — GET `/tasks` with a filter — only high priority](#s4) |
| 5 | [TEST 5 — GET `/tasks` with two filters at once](#s5) |
| 6 | [TEST 6 — GET `/tasks/{task_id}` — Get task number 1](#s6) |
| 7 | [TEST 7 — GET `/tasks/{task_id}` — Task that does not exist](#s7) |
| 8 | [TEST 8 — POST `/tasks` — Create a complete task](#s8) |
| 9 | [TEST 9 — POST `/tasks` — Create a minimal task](#s9) |
| 10 | [TEST 10 — POST `/tasks` — Intentional error (missing title)](#s10) |
| 11 | [TEST 11 — GET `/tasks` again — confirm the new tasks are there](#s11) |
| 12 | [TEST 12 — PUT `/tasks/{task_id}` — Replace task 1 entirely](#s12) |
| 13 | [TEST 13 — PATCH `/tasks/{task_id}` — Mark task 3 as completed](#s13) |
| 14 | [TEST 14 — PATCH `/tasks/{task_id}` — Change only the priority](#s14) |
| 15 | [TEST 15 — DELETE `/tasks/{task_id}` — Delete task 4](#s15) |
| 16 | [TEST 16 — GET `/tasks/{task_id}` — Confirm the deletion](#s16) |
| 17 | [TEST 17 — DELETE again — task already deleted](#s17) |
| 18 | [Final Check — GET `/tasks` — See the final state](#s18) |

---

<a id="s0"></a>

<details>
<summary>0 — Start the server and open Swagger UI</summary>

<br/>

### A — Open a terminal

In VS Code, press **`Ctrl + `` `** (backtick key — next to the 1 key).

A terminal panel opens at the bottom of the screen.

---

### B — Navigate to the project folder

Type this command and press **Enter**:

```powershell
cd "c:\00-projetsGA\2025H-420-911-MA-main -COURSES EN ANGLAIS\inskillflow-docs-portfolio-1\mini_fastapi"
```

---

### C — Activate the virtual environment

```powershell
venv\Scripts\activate
```

After pressing Enter, your prompt changes to:

```text
(venv) PS C:\...\mini_fastapi>
```

> If you see an error about "running scripts is disabled", run this once:
> ```powershell
> Set-ExecutionPolicy -ExecutionPolicy RemoteSigned -Scope CurrentUser
> ```
> Then try `venv\Scripts\activate` again.

---

### D — Start the FastAPI server

```bash
uvicorn main:app --reload
```

Press **Enter**. You should see:

```text
INFO:     Uvicorn running on http://127.0.0.1:8000 (Press CTRL+C to quit)
INFO:     Started reloader process [...]
INFO:     Application startup complete.
```

> ⚠️ **Do not close this terminal.** The server stops if you close it.
> Open a second terminal for other commands if needed (`Ctrl + `` ` then click the `+` button).

---

### E — Open Swagger UI in your browser

Open your web browser (Chrome, Edge, Firefox — any browser works).

Type this address in the address bar and press **Enter**:

```text
http://127.0.0.1:8000/docs
```

---

### F — What you should see

You will see a page titled **"Task Manager API"** with colored buttons.

Each button is one endpoint (one route of the API).

The page should show these buttons, in this order:

```
GET    /           Root — API info
GET    /tasks      Get all tasks
GET    /tasks/{task_id}   Get one task by ID
POST   /tasks      Create a new task
PUT    /tasks/{task_id}   Replace a task entirely (PUT)
PATCH  /tasks/{task_id}   Partially update a task (PATCH)
DELETE /tasks/{task_id}   Delete a task
```

---

### Color guide — what each color means

| Color | HTTP Method | What it does |
|---|---|---|
| 🟢 **Green** | GET | Read — never changes anything |
| 🟡 **Yellow/brown** | POST | Create — adds a new record |
| 🔵 **Blue** | PUT | Replace — overwrites everything |
| 🟣 **Purple/grey** | PATCH | Partial update — changes only specific fields |
| 🔴 **Red** | DELETE | Delete — removes a record permanently |

---

> ✅ You can see the Swagger UI page with all 7 endpoints?
> Perfect — move to Test 1.

</details>

<p align="right"><a href="#top">↑ Back to top</a></p>

---

<a id="s1"></a>

<details>
<summary>TEST 1 — GET `/` — Is the server alive?</summary>

<br/>

### What this test does

You are asking the server: "Are you running?"
The server replies with a short message and the number of tasks.

---

### Step 1 — Find the button

On the Swagger UI page, look for the **first green button** at the top:

```
GET   /   Root — API info
```

**Click on that green button.**

The panel expands downward.

---

### Step 2 — Click "Try it out"

Inside the expanded panel, look for a button that says:

```
Try it out
```

It is on the **right side** of the panel.

**Click it.**

The button changes to **"Cancel"** — this means you are now in interactive mode.

---

### Step 3 — Click "Execute"

You will see a large blue button:

```
Execute
```

**Click it.**

---

### Step 4 — Read the response

Scroll down a little inside the panel. You will see a section called **"Responses"**.

Look at the **"Response body"** box. It should contain:

```json
{
  "message": "Task Manager API is running",
  "docs": "http://127.0.0.1:8000/docs",
  "total_tasks": 4
}
```

Also check the **"Code"** column — it should say:

```
200
```

---

### What this means

| Field | Value | Explanation |
|---|---|---|
| `message` | "Task Manager API is running" | The server is alive and working |
| `docs` | "http://127.0.0.1:8000/docs" | The link to this Swagger page |
| `total_tasks` | 4 | There are currently 4 tasks in memory |
| Code | 200 | 200 = success |

---

> ✅ You got a 200 response with `total_tasks: 4`?
> Perfect — move to Test 2.

> ❌ You see an error? The server is not running. Go back to step 0 and run `uvicorn main:app --reload`.

</details>

<p align="right"><a href="#top">↑ Back to top</a></p>

---

<a id="s2"></a>

<details>
<summary>TEST 2 — GET `/tasks` — List all tasks</summary>

<br/>

### What this test does

You are asking the server: "Give me all the tasks."
The server replies with a list of all tasks in memory.

---

### Step 1 — Find the button

Look for the **second green button**:

```
GET   /tasks   Get all tasks
```

**Click on it.**

---

### Step 2 — Click "Try it out"

Click the **"Try it out"** button on the right.

---

### Step 3 — Leave the filters empty

You will see two fields:
- `completed`
- `priority`

**Leave both fields completely empty.** Do not type anything.

---

### Step 4 — Click "Execute"

Click the blue **"Execute"** button.

---

### Step 5 — Read the response

The **"Response body"** should contain a list of **4 tasks**:

```json
[
  {
    "id": 1,
    "title": "Learn FastAPI",
    "description": "Read the official FastAPI documentation",
    "completed": false,
    "priority": "high",
    "created_at": "2026-03-19 08:00:00"
  },
  {
    "id": 2,
    "title": "Build a REST API",
    "description": "Create a CRUD API with GET, POST, PUT, DELETE",
    "completed": true,
    "priority": "high",
    "created_at": "2026-03-19 09:00:00"
  },
  {
    "id": 3,
    "title": "Write unit tests",
    "description": "Use pytest and FastAPI TestClient",
    "completed": false,
    "priority": "medium",
    "created_at": "2026-03-19 10:00:00"
  },
  {
    "id": 4,
    "title": "Deploy to production",
    "description": "Use Docker and a cloud provider",
    "completed": false,
    "priority": "low",
    "created_at": "2026-03-19 11:00:00"
  }
]
```

The **response code** should be **200**.

---

### What to notice

- The response starts with `[` and ends with `]` — that means it is a **list** (array) of tasks
- Each task is wrapped in `{` and `}` — that is a **JSON object**
- There are exactly **4 tasks** — IDs 1, 2, 3, 4
- Only task 2 (`"Build a REST API"`) has `"completed": true`
- Task 2 has `"priority": "high"` — same as task 1
- Task 3 has `"priority": "medium"`
- Task 4 has `"priority": "low"`

---

> ✅ You see a list of 4 tasks with code 200?
> Perfect — move to Test 3.

</details>

<p align="right"><a href="#top">↑ Back to top</a></p>

---

<a id="s3"></a>

<details>
<summary>TEST 3 — GET `/tasks` with a filter — only completed tasks</summary>

<br/>

### What this test does

You are asking the server: "Give me only the tasks that are completed."
This uses a **query parameter** — an extra option you add to the request.

---

### Step 1 — The GET /tasks button is still open

If you closed it, click **GET /tasks** again and click **"Try it out"**.

---

### Step 2 — Fill in the `completed` field

You see the `completed` field. Click on it and type:

```
true
```

Leave the `priority` field **empty**.

---

### Step 3 — Click "Execute"

Click the blue **"Execute"** button.

---

### Step 4 — Read the response

Look at the **"Request URL"** line — it should show:

```
http://127.0.0.1:8000/tasks?completed=true
```

Notice the `?completed=true` at the end — that is your filter.

The **"Response body"** should contain **only 1 task**:

```json
[
  {
    "id": 2,
    "title": "Build a REST API",
    "description": "Create a CRUD API with GET, POST, PUT, DELETE",
    "completed": true,
    "priority": "high",
    "created_at": "2026-03-19 09:00:00"
  }
]
```

---

### Step 5 — Now try the opposite: completed = false

Change the `completed` field to:

```
false
```

Click **"Execute"** again.

You should get **3 tasks** — IDs 1, 3, and 4 (the ones that are NOT completed).

---

### What to notice

- The `?completed=true` at the end of the URL is called a **query parameter**
- The server uses it to filter the list
- `completed=true` → only task 2
- `completed=false` → tasks 1, 3, and 4

---

> ✅ You see 1 task when filtering `true`, and 3 tasks when filtering `false`?
> Perfect — move to Test 4.

</details>

<p align="right"><a href="#top">↑ Back to top</a></p>

---

<a id="s4"></a>

<details>
<summary>TEST 4 — GET `/tasks` with a filter — only high priority</summary>

<br/>

### What this test does

You are asking the server: "Give me only the tasks with priority = high."

---

### Step 1 — Still in GET /tasks

If needed, click **GET /tasks** → **Try it out**.

---

### Step 2 — Fill in the `priority` field

- Clear the `completed` field (delete any text in it — leave it completely empty)
- In the `priority` field, type:

```
high
```

---

### Step 3 — Click "Execute"

Click **"Execute"**.

---

### Step 4 — Read the response

The **"Request URL"** should show:

```
http://127.0.0.1:8000/tasks?priority=high
```

The response body should contain **2 tasks** — IDs 1 and 2:

```json
[
  {
    "id": 1,
    "title": "Learn FastAPI",
    "completed": false,
    "priority": "high",
    ...
  },
  {
    "id": 2,
    "title": "Build a REST API",
    "completed": true,
    "priority": "high",
    ...
  }
]
```

---

### Try the other priority values

**Try `priority = medium`:**
- You should get **1 task** — task 3 "Write unit tests"

**Try `priority = low`:**
- You should get **1 task** — task 4 "Deploy to production"

---

> ✅ You see 2 tasks for `high`, 1 for `medium`, 1 for `low`?
> Perfect — move to Test 5.

</details>

<p align="right"><a href="#top">↑ Back to top</a></p>

---

<a id="s5"></a>

<details>
<summary>TEST 5 — GET `/tasks` with two filters at once</summary>

<br/>

### What this test does

You can combine both filters at the same time.
You are asking: "Give me only the tasks that are NOT completed AND have high priority."

---

### Step 1 — Still in GET /tasks

If needed, click **GET /tasks** → **Try it out**.

---

### Step 2 — Fill in BOTH fields

- `completed` field → type: `false`
- `priority` field → type: `high`

---

### Step 3 — Click "Execute"

---

### Step 4 — Read the response

The **"Request URL"** should show:

```
http://127.0.0.1:8000/tasks?completed=false&priority=high
```

Notice the `&` between the two filters — it means "AND".

The response body should contain **1 task only** — task 1:

```json
[
  {
    "id": 1,
    "title": "Learn FastAPI",
    "completed": false,
    "priority": "high",
    ...
  }
]
```

Why only task 1?
- Task 1: `completed=false` ✅ and `priority=high` ✅ → included
- Task 2: `completed=true` ❌ → excluded (we asked for `false`)
- Task 3: `priority=medium` ❌ → excluded (we asked for `high`)
- Task 4: `priority=low` ❌ → excluded (we asked for `high`)

---

> ✅ You see exactly 1 task — "Learn FastAPI"?
> Perfect — move to Test 6.

</details>

<p align="right"><a href="#top">↑ Back to top</a></p>

---

<a id="s6"></a>

<details>
<summary>TEST 6 — GET `/tasks/{task_id}` — Get task number 1</summary>

<br/>

### What this test does

You are asking the server: "Give me the task with ID number 1."
This is different from listing all tasks — you get exactly **one** task by its ID.

---

### Step 1 — Find the button

Look for the **third green button**:

```
GET   /tasks/{task_id}   Get one task by ID
```

**Click on it.**

---

### Step 2 — Click "Try it out"

Click **"Try it out"** on the right.

---

### Step 3 — Enter the task ID

You will see a field labeled:

```
task_id *   (integer)
```

The `*` means this field is **required** — you must fill it in.

Click on the field and type:

```
1
```

---

### Step 4 — Click "Execute"

---

### Step 5 — Read the response

The **"Request URL"** should show:

```
http://127.0.0.1:8000/tasks/1
```

The response body should contain **one task** (not a list):

```json
{
  "id": 1,
  "title": "Learn FastAPI",
  "description": "Read the official FastAPI documentation",
  "completed": false,
  "priority": "high",
  "created_at": "2026-03-19 08:00:00"
}
```

Notice: the response starts with `{` not `[` — it is a **single object**, not a list.

The response code is **200**.

---

### Step 6 — Try other IDs

Try these IDs one at a time — click Execute after each one:

| task_id | Expected title |
|---|---|
| `2` | "Build a REST API" |
| `3` | "Write unit tests" |
| `4` | "Deploy to production" |

---

> ✅ You get the correct task for each ID?
> Perfect — move to Test 7.

</details>

<p align="right"><a href="#top">↑ Back to top</a></p>

---

<a id="s7"></a>

<details>
<summary>TEST 7 — GET `/tasks/{task_id}` — Task that does not exist</summary>

<br/>

### What this test does

You are going to ask for a task that **does not exist**.
This is intentional — you want to see what the server does when you ask for something that is not there.

---

### Step 1 — Still in GET /tasks/{task_id}

If needed, click **GET /tasks/{task_id}** → **Try it out**.

---

### Step 2 — Enter a non-existent ID

In the `task_id` field, type:

```
99
```

There is no task with ID 99 in the database.

---

### Step 3 — Click "Execute"

---

### Step 4 — Read the response

The response code should be **404** (shown in red in Swagger UI).

The response body should say:

```json
{
  "detail": "Task with ID 99 not found"
}
```

---

### What 404 means

> **404 = Not Found**
> The resource you asked for does not exist.
> This is the server's way of saying "I looked — it's not here."

This is NOT a server crash — it is expected behavior. The API was programmed to return a 404 when the ID does not exist.

---

### Try a few more non-existent IDs

| task_id | Expected response |
|---|---|
| `0` | 404 — "Task with ID 0 not found" |
| `100` | 404 — "Task with ID 100 not found" |
| `999` | 404 — "Task with ID 999 not found" |

---

> ✅ You see a 404 response with the message "Task with ID 99 not found"?
> Perfect — move to Test 8.

</details>

<p align="right"><a href="#top">↑ Back to top</a></p>

---

<a id="s8"></a>

<details>
<summary>TEST 8 — POST `/tasks` — Create a complete task</summary>

<br/>

### What this test does

You are going to **create a new task** by sending data to the server.
This is the first test where you send data — the previous tests only read data.

---

### Step 1 — Find the button

Look for the **yellow/brown button**:

```
POST   /tasks   Create a new task
```

**Click on it.**

---

### Step 2 — Click "Try it out"

Click **"Try it out"** on the right.

---

### Step 3 — Look at the Request body

You will see a large text area called **"Request body"** with some example JSON already filled in.

It looks like this:
```json
{
  "title": "string",
  "description": "",
  "completed": false,
  "priority": "medium"
}
```

This is just a template. You need to replace it with your own data.

---

### Step 4 — Replace the content completely

Click inside the text area. **Select all** (`Ctrl+A`) and **delete** everything.

Then type this **exactly** (copy-paste is fine):

```json
{
  "title": "Study for the exam",
  "description": "Review chapters 3 to 7",
  "completed": false,
  "priority": "high"
}
```

> ⚠️ Important rules for JSON:
> - Use **double quotes** `"` — NOT single quotes `'`
> - `false` and `true` are **lowercase** — NOT `False` or `True`
> - Do NOT put a comma after the last field
> - Do NOT forget the opening `{` and closing `}`

---

### Step 5 — Click "Execute"

---

### Step 6 — Read the response

The response code should be **201** (shown in green).

> **201 = Created**
> The task was successfully created.

The response body should show your new task with a new ID assigned by the server:

```json
{
  "id": 5,
  "title": "Study for the exam",
  "description": "Review chapters 3 to 7",
  "completed": false,
  "priority": "high",
  "created_at": "2026-03-30 14:22:05"
}
```

Notice:
- The server automatically assigned `"id": 5`
- The server automatically added `"created_at"` with the current date and time
- These two fields were NOT in what you sent — the server adds them

---

> ✅ You see a 201 response with `"id": 5` and a `created_at` timestamp?
> Perfect — move to Test 9.

</details>

<p align="right"><a href="#top">↑ Back to top</a></p>

---

<a id="s9"></a>

<details>
<summary>TEST 9 — POST `/tasks` — Create a minimal task</summary>

<br/>

### What this test does

You are going to create a task with **only the required field** — just the `title`.
The other fields will use their **default values**.

---

### Step 1 — Still in POST /tasks

If needed, click **POST /tasks** → **Try it out**.

---

### Step 2 — Enter only the title

In the Request body, **select all and delete** the previous content.

Type this:

```json
{
  "title": "Quick reminder"
}
```

Only the `title` field — nothing else.

---

### Step 3 — Click "Execute"

---

### Step 4 — Read the response

Response code: **201**

Response body:

```json
{
  "id": 6,
  "title": "Quick reminder",
  "description": "",
  "completed": false,
  "priority": "medium",
  "created_at": "2026-03-30 14:23:11"
}
```

Notice the **default values** that were applied automatically:
- `"description"` → `""` (empty string — the default)
- `"completed"` → `false` (the default)
- `"priority"` → `"medium"` (the default)

You did not send these fields — the server filled them in with defaults.

---

> ✅ You see a 201 response with `"id": 6` and default values for the missing fields?
> Perfect — move to Test 10.

</details>

<p align="right"><a href="#top">↑ Back to top</a></p>

---

<a id="s10"></a>

<details>
<summary>TEST 10 — POST `/tasks` — Intentional error (missing title)</summary>

<br/>

### What this test does

You are going to send a broken request **on purpose** to see what happens when the data is invalid.
`title` is required — if you don't send it, the server must refuse the request.

---

### Step 1 — Still in POST /tasks

If needed, click **POST /tasks** → **Try it out**.

---

### Step 2 — Send an empty body

In the Request body, **select all and delete** everything.

Type this:

```json
{}
```

Just two curly braces — completely empty.

---

### Step 3 — Click "Execute"

---

### Step 4 — Read the response

Response code: **422** (shown in red).

> **422 = Unprocessable Entity**
> The server received your request, understood it, but the data is **invalid**.
> In this case: `title` is missing.

The response body will look like this:

```json
{
  "detail": [
    {
      "type": "missing",
      "loc": ["body", "title"],
      "msg": "Field required",
      "input": {}
    }
  ]
}
```

Read the message carefully:
- `"loc": ["body", "title"]` → the problem is in the body, field `title`
- `"msg": "Field required"` → `title` is mandatory, you must provide it

---

### Step 5 — Try another broken body

Try sending data with a wrong type — `completed` should be a boolean (`true`/`false`), but you send a string:

```json
{
  "title": "Test task",
  "completed": "yes"
}
```

Click **Execute**.

You get another **422** — this time about the `completed` field having the wrong type.

---

> ✅ You see a 422 for the empty body and another 422 for the wrong type?
> Perfect — move to Test 11.

</details>

<p align="right"><a href="#top">↑ Back to top</a></p>

---

<a id="s11"></a>

<details>
<summary>TEST 11 — GET `/tasks` again — confirm the new tasks are there</summary>

<br/>

### What this test does

After creating 2 new tasks (Tests 8 and 9), you go back to check the full list.
You want to confirm the tasks were actually saved.

---

### Step 1 — Click on GET /tasks

Click the **GET /tasks** green button.

Click **"Try it out"**.

---

### Step 2 — Leave everything empty

Do NOT fill in `completed` or `priority`. Leave both empty.

---

### Step 3 — Click "Execute"

---

### Step 4 — Read the response

You should now see **6 tasks** — the original 4 plus the 2 you just created:

| ID | Title |
|---|---|
| 1 | Learn FastAPI |
| 2 | Build a REST API |
| 3 | Write unit tests |
| 4 | Deploy to production |
| 5 | Study for the exam ← **you created this in Test 8** |
| 6 | Quick reminder ← **you created this in Test 9** |

---

> ✅ You see 6 tasks total including your 2 new ones?
> Perfect — move to Test 12.

> ❌ You still see only 4 tasks? The server may have been restarted. Go back to Tests 8 and 9.

</details>

<p align="right"><a href="#top">↑ Back to top</a></p>

---

<a id="s12"></a>

<details>
<summary>TEST 12 — PUT `/tasks/{task_id}` — Replace task 1 entirely</summary>

<br/>

### What this test does

**PUT** replaces a task **completely**.
Every single field is overwritten with the new data you send.
Think of it as: "Delete what was there and put this new thing instead."

---

### Step 1 — Find the button

Look for the **blue button**:

```
PUT   /tasks/{task_id}   Replace a task entirely (PUT)
```

**Click on it.**

---

### Step 2 — Click "Try it out"

---

### Step 3 — Enter the task ID

In the `task_id` field, type:

```
1
```

You are going to replace task 1 ("Learn FastAPI").

---

### Step 4 — Enter the new data

In the **Request body**, **select all and delete** everything.

Type this:

```json
{
  "title": "Master FastAPI completely",
  "description": "Build 3 real projects from scratch",
  "completed": false,
  "priority": "high"
}
```

---

### Step 5 — Click "Execute"

---

### Step 6 — Read the response

Response code: **200**

Response body:

```json
{
  "id": 1,
  "title": "Master FastAPI completely",
  "description": "Build 3 real projects from scratch",
  "completed": false,
  "priority": "high",
  "created_at": "2026-03-19 08:00:00"
}
```

Notice:
- `"id"` stays `1` — the ID never changes
- `"created_at"` stays `"2026-03-19 08:00:00"` — the original creation date is preserved
- Everything else was **completely replaced** with your new data

---

### Step 7 — Verify: read task 1 again

Go to **GET /tasks/{task_id}** → Try it out → `task_id = 1` → Execute.

You should see the updated title: "Master FastAPI completely".

---

### What happens if you send only part of the data with PUT?

Try this — send a PUT with only the title:

```json
{
  "title": "Just a title"
}
```

Click Execute.

You will get a **422 error** — `title` is required, BUT for PUT all fields need to be valid.

Actually wait — `title` IS the only required field. The others have defaults.

So if you send:
```json
{
  "title": "Just a title"
}
```

The response will be 200, but `description` resets to `""`, `completed` resets to `false`, `priority` resets to `"medium"`.

**This is the key difference between PUT and PATCH:**
- PUT: everything resets to defaults if you don't send it
- PATCH (next test): only what you send is changed

---

> ✅ You see the task 1 title changed to "Master FastAPI completely" with code 200?
> Perfect — move to Test 13.

</details>

<p align="right"><a href="#top">↑ Back to top</a></p>

---

<a id="s13"></a>

<details>
<summary>TEST 13 — PATCH `/tasks/{task_id}` — Mark task 3 as completed</summary>

<br/>

### What this test does

**PATCH** updates **only the fields you send**.
All other fields stay exactly as they were.
Think of it as: "Change only this one thing — leave everything else alone."

---

### Step 1 — First, read task 3 so you know what it looks like

Go to **GET /tasks/{task_id}** → Try it out → `task_id = 3` → Execute.

Write down what you see:

```json
{
  "id": 3,
  "title": "Write unit tests",
  "description": "Use pytest and FastAPI TestClient",
  "completed": false,
  "priority": "medium",
  "created_at": "2026-03-19 10:00:00"
}
```

`completed` is currently `false`. You are going to change it to `true`.

---

### Step 2 — Find the PATCH button

Look for the **purple/grey button**:

```
PATCH   /tasks/{task_id}   Partially update a task (PATCH)
```

**Click on it.**

---

### Step 3 — Click "Try it out"

---

### Step 4 — Enter the task ID

In the `task_id` field, type:

```
3
```

---

### Step 5 — Enter only the field you want to change

In the **Request body**, **select all and delete** everything.

Type this:

```json
{
  "completed": true
}
```

**Only one field.** That is intentional — PATCH only needs the fields you want to change.

---

### Step 6 — Click "Execute"

---

### Step 7 — Read the response

Response code: **200**

Response body:

```json
{
  "id": 3,
  "title": "Write unit tests",
  "description": "Use pytest and FastAPI TestClient",
  "completed": true,
  "priority": "medium",
  "created_at": "2026-03-19 10:00:00"
}
```

Notice what changed and what did NOT change:

| Field | Before | After |
|---|---|---|
| `title` | "Write unit tests" | "Write unit tests" ← **unchanged** |
| `description` | "Use pytest..." | "Use pytest..." ← **unchanged** |
| `completed` | `false` | `true` ← **YOU CHANGED THIS** |
| `priority` | "medium" | "medium" ← **unchanged** |
| `created_at` | "2026-03-19 10:00:00" | "2026-03-19 10:00:00" ← **unchanged** |

Only `completed` changed. Everything else stayed exactly the same.

---

> ✅ You see `"completed": true` for task 3 while all other fields are unchanged?
> Perfect — move to Test 14.

</details>

<p align="right"><a href="#top">↑ Back to top</a></p>

---

<a id="s14"></a>

<details>
<summary>TEST 14 — PATCH `/tasks/{task_id}` — Change only the priority</summary>

<br/>

### What this test does

Another PATCH test — this time you change only the `priority` field.
This confirms that PATCH really does leave everything else untouched.

---

### Step 1 — Still in PATCH /tasks/{task_id}

If needed, click **PATCH /tasks/{task_id}** → **Try it out**.

---

### Step 2 — Enter the task ID

In the `task_id` field, type:

```
2
```

---

### Step 3 — Enter only the priority

In the **Request body**, **select all and delete** everything.

Type this:

```json
{
  "priority": "low"
}
```

---

### Step 4 — Click "Execute"

---

### Step 5 — Read the response

Response code: **200**

You should see task 2 with `"priority": "low"` — everything else unchanged:

```json
{
  "id": 2,
  "title": "Build a REST API",
  "description": "Create a CRUD API with GET, POST, PUT, DELETE",
  "completed": true,
  "priority": "low",
  "created_at": "2026-03-19 09:00:00"
}
```

`priority` changed from `"high"` to `"low"`. `title`, `description`, `completed`, `created_at` — all untouched.

---

### Step 6 — Try changing two fields at once

PATCH also lets you change multiple fields in one request.

`task_id = 1`, body:

```json
{
  "completed": true,
  "priority": "medium"
}
```

Click Execute.

Both `completed` AND `priority` change for task 1. Everything else stays the same.

---

> ✅ You successfully changed only the priority of task 2 with code 200?
> Perfect — move to Test 15.

</details>

<p align="right"><a href="#top">↑ Back to top</a></p>

---

<a id="s15"></a>

<details>
<summary>TEST 15 — DELETE `/tasks/{task_id}` — Delete task 4</summary>

<br/>

### What this test does

You are going to **permanently delete** a task.
The task will be removed from memory and cannot be recovered (unless you restart the server).

---

### Step 1 — Find the button

Look for the **red button**:

```
DELETE   /tasks/{task_id}   Delete a task
```

**Click on it.**

---

### Step 2 — Click "Try it out"

---

### Step 3 — Enter the task ID

In the `task_id` field, type:

```
4
```

You are going to delete task 4 ("Deploy to production").

---

### Step 4 — Click "Execute"

---

### Step 5 — Read the response

The response code should be **204**.

> **204 = No Content**
> The task was deleted successfully.
> The server has nothing to return — that is why the body is empty.

Look at the **Response body** — it is completely empty. **This is normal and correct.**

A 204 with an empty body = successful deletion.

---

### Important — 204 is success even though there is no body

Some beginners think an empty response means an error. It does not.
- 200 = success with data
- 201 = success, new resource created
- **204 = success, nothing to return (delete worked)**

---

> ✅ You see a 204 response with an empty body?
> Perfect — move to Test 16.

</details>

<p align="right"><a href="#top">↑ Back to top</a></p>

---

<a id="s16"></a>

<details>
<summary>TEST 16 — GET `/tasks/{task_id}` — Confirm the deletion</summary>

<br/>

### What this test does

After deleting task 4, you try to read it.
The server should say it does not exist anymore.

---

### Step 1 — Go to GET /tasks/{task_id}

Click **GET /tasks/{task_id}** → **Try it out**.

---

### Step 2 — Enter the ID of the deleted task

In the `task_id` field, type:

```
4
```

---

### Step 3 — Click "Execute"

---

### Step 4 — Read the response

Response code: **404**

Response body:

```json
{
  "detail": "Task with ID 4 not found"
}
```

Task 4 is gone. The server confirms it no longer exists.

---

### Step 5 — Verify the full list

Go to **GET /tasks** → Try it out → Execute (leave filters empty).

You should see **5 tasks** — IDs 1, 2, 3, 5, 6.
Task 4 is not in the list anymore.

---

> ✅ You get a 404 for task 4 and see 5 tasks in the full list?
> Perfect — move to Test 17.

</details>

<p align="right"><a href="#top">↑ Back to top</a></p>

---

<a id="s17"></a>

<details>
<summary>TEST 17 — DELETE again — task already deleted</summary>

<br/>

### What this test does

You try to delete task 4 **again** — even though it was already deleted.
The server should return a 404 because there is nothing to delete.

---

### Step 1 — Go to DELETE /tasks/{task_id}

Click **DELETE /tasks/{task_id}** → **Try it out**.

---

### Step 2 — Enter the same ID

`task_id` = `4`

---

### Step 3 — Click "Execute"

---

### Step 4 — Read the response

Response code: **404**

Response body:

```json
{
  "detail": "Task with ID 4 not found"
}
```

The server cannot delete something that does not exist — it returns 404.

This behavior is called **idempotent safety** — deleting something that is already gone is handled gracefully, not with a crash.

---

> ✅ You see a 404 when trying to delete an already-deleted task?
> Perfect — move to the Final Check.

</details>

<p align="right"><a href="#top">↑ Back to top</a></p>

---

<a id="s18"></a>

<details>
<summary>Final Check — GET `/tasks` — See the final state</summary>

<br/>

### What this test does

You run one last GET to see the final state of the database after all your tests.

---

### Step 1 — Go to GET /tasks

Click **GET /tasks** → **Try it out**.

Leave `completed` and `priority` empty.

Click **Execute**.

---

### What you should see

A list of **5 tasks** (task 4 was deleted):

| ID | Title | Completed | Priority |
|---|---|---|---|
| 1 | Master FastAPI completely | true | medium |
| 2 | Build a REST API | true | low |
| 3 | Write unit tests | true | medium |
| 5 | Study for the exam | false | high |
| 6 | Quick reminder | false | medium |

> Your exact values may differ slightly depending on what you changed during the PATCH tests.

---

### Summary of everything that changed during your tests

| Test | What happened |
|---|---|
| Test 8 | Created task 5 "Study for the exam" |
| Test 9 | Created task 6 "Quick reminder" |
| Test 12 | Replaced task 1 → title is now "Master FastAPI completely" |
| Test 13 | Patched task 3 → `completed` is now `true` |
| Test 14 | Patched task 2 → `priority` is now `"low"` |
| Test 15 | Deleted task 4 |

---

### All 18 tests are done

You have successfully tested every endpoint of the Task Manager API using Swagger UI:

| Method | Route | Tested |
|---|---|---|
| GET | `/` | ✅ Test 1 |
| GET | `/tasks` | ✅ Tests 2, 3, 4, 5, 11, Final |
| GET | `/tasks/{id}` | ✅ Tests 6, 7, 16 |
| POST | `/tasks` | ✅ Tests 8, 9, 10 |
| PUT | `/tasks/{id}` | ✅ Test 12 |
| PATCH | `/tasks/{id}` | ✅ Tests 13, 14 |
| DELETE | `/tasks/{id}` | ✅ Tests 15, 17 |

---

### Want to reset and start over?

The data lives only in memory. To reset to the original 4 tasks:

1. Go to the terminal where uvicorn is running
2. Press `Ctrl + C` to stop the server
3. Run `uvicorn main:app --reload` again
4. All data is back to the original 4 tasks

</details>

<p align="right"><a href="#top">↑ Back to top</a></p>

---

<p align="center">
  <strong>End of Swagger UI Step-by-Step Guide</strong><br/>
  <a href="#top">↑ Back to the top</a>
</p>
