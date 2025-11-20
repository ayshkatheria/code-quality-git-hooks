# code-quality-git-hooks

#🔧 Step 1 — Install flake8

Make sure flake8 is installed on your system:
>pip install flake8

Verify:
>flake8 --version

#📁 Step 2 — Create a Pre-Commit Hook

Git hooks live inside:
.yourproject/.git/hooks/

Create a file called pre-commit inside that folder:
>touch/vim .git/hooks/pre-commit

#✍️ Step 3 — Add flake8 Hook Script

Open the file and paste this script:
#!/bin/bash
# Run flake8 only on staged Python files
# Collect staged .py files
files=$(git diff --cached --name-only --diff-filter=ACM | grep '\.py$')
# If no Python files staged, exit
if [ -z "$files" ]; then
    exit 0
fi
echo "Running flake8 on staged Python files..."
flake8 $files
status=$?
if [ $status -ne 0 ]; then
    echo "❌ flake8 failed! Please fix the issues before committing."
    exit 1
fi
echo "✔ flake8 passed successfully."
exit 0

#🔐 Step 4 — Make the Hook Executable

Git will not run the script unless it is executable:
>chmod +x .git/hooks/pre-commit

#🚀 Step 5 — Test Your Setup

Make a small change, stage the file, and commit:
>git add .
>git commit -m "Test flake8 hook"

If code has lint issues → commit will be blocked.
If clean → commit will succeed.

🎉 Done!

Your project now automatically enforces flake8 for all staged Python files before every commit.





