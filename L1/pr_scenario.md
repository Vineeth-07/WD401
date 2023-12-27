## Handling Code Review Feedback

### Frontend code review

Code Snippet 1: React Component

```jsx
function DisplayResult({ data }) {
  return <div>{data}</div>;
}
```

Feedback: During the frontend code review, feedback suggest the need for more concise JSX and improved error handling.

Revised react component

```jsx
function DisplayResult({ data }) {
  if (!data) {
    return <div>No data available</div>;
  }

  return <div>{data}</div>;
}
```

### Backend code review

Code snippet 2: Node.js route

```javascript
app.get("/api/result", (req, res) => {
  res.json({ result: calculatedResult });
});
```

Feedback: During the backend code review, feedback suggest the need for improved input validation and the use of proper HTTP status codes.

Revised Node.js route

```javascript
app.get("/api/result/:input", (req, res) => {
  const input = parseInt(req.params.input);

  if (isNaN(input)) {
    return res.status(400).json({ error: "Invalid input, must be a number." });
  }

  const calculatedResult = calculateResult(input);
  return res.status(200).json({ result: calculatedResult });
});
```

## Iterative Development Process

![Flow Chart](<Iterative development.jpg>)

Step 1 - **Initial implementation:** Start working on the initial implementation in a feature branch.

Step 2 - **Code review:** Submit a pull request for code review.

Step 3 - **Submit pull request:** Pull request is submitted for code review.

Step 4 - **Feedback:** If feedback not received then merge the code to the develop branch. If feedback is received, engage in iterative development to address feedback.

Step 5 - **Code approval:** Repeat the steps untill the code is approved.

Step 6 - **Merge to develop:** The approved code is merged into the main development branch.

## Resolving merge conflicts

Merge conflicts occur when individuals make conflicting modifications to the same line within a file or when one person edits a file while another person deletes the same file.

Original feature branch:

```jsx
function FeatureComponent() {
  return <div>Feature component</div>;
}
```

Conflicting changes on master:

```jsx
function FeatureComponent() {
  return <div>Updated feature component</div>;
}
```

### Steps to resolve merge conflicts

1. Pull the latest changes from the master branch

```bash
git pull origin master

```

2. Open conflicting file and resolve conflicts manually in the file.

```jsx
function FeatureComponent() {
  return <div>Feature component</div>;
}
```

3. Add the resolved file.

```bash
git add <file_name>
```

4. Continue with the merge

```bash
git merge master
```

## CI/CD Integration

Consider a login function that returns a user role based on the provided credentials:

```javascript
function login(username, password) {
  if (username === "admin" && password === "password123") {
    return "Admin";
  } else if (username === "user" && password === "123456") {
    return "Regular User";
  } else {
    return "Invalid credentials";
  }
}
```

Now, let's create a test case for the updated login function:

```javascript
test("login function - Admin User", () => {
  const res = login("admin", "password123");
  expect(res).toBe("Admin");
});

test("login function - Regular User", () => {
  const res = login("user", "123456");
  expect(res).toBe("Regular User");
});

test("login function - Invalid Credentials", () => {
  const res = login("invalid", "invalid");
  expect(res).toBe("Invalid credentials");
});
```

CI/CD Configuration:

```yaml
on:
  push:
    branches:
      - main

jobs:
  test_and_lint:
    runs-on: ubuntu-latest

    steps:
      - name: Repository
        uses: actions/checkout@v2

      - name: Setup Node.js
        uses: actions/setup-node@v3
        with:
          node-version: "20"

      - name: Install Dependencies
        run: npm install

      - name: Lint Code
        run: npm run lint

      - name: Run Tests
        run: npm test
```
