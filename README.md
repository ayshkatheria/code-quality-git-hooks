🚀 1. Install flake8

Run the following command depending on your OS:

Windows
py -m pip install flake8

Linux / macOS
pip3 install flake8


Verify installation:

flake8 --version

📁 2. Create the pre-commit hook

Go to your project root and open:

.git/hooks/


Create a file named:

pre-commit

✍️ 3. Add the following code inside .git/hooks/pre-commit
#!/bin/bash

# Get all staged Python files
files=$(git diff --cached --name-only --diff-filter=ACM | grep '\.py$')

# If no Python files are staged, exit
if [ -z "$files" ]; then
    exit 0
fi

echo "Running flake8 on staged Python files..."

# Run flake8 on the staged files
flake8 $files
status=$?

if [ $status -ne 0 ]; then
    echo "❌ flake8 failed. Fix the errors before committing."
    exit 1
fi

echo "✔ flake8 passed successfully!"
exit 0

🔐 4. Make the hook executable
Linux / macOS
chmod +x .git/hooks/pre-commit

Windows (Git Bash)
git update-index --chmod=+x .git/hooks/pre-commit

🧪 5. Test the hook

Add a file and try committing:

git add your_file.py
git commit -m "Test flake8 hook"


If flake8 finds lint issues → commit will stop until fixed.
If no issues → commit will pass.

🎉 Done!

You now have an automated flake8 Python linter that runs every time you commit code.
This ensures clean, consistent, and error-free Python code moving forward.
