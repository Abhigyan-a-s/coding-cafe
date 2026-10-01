Question 1: Meaning of --global in git config and omitting it

--global: Applies settings system-wide across all Git repositories for your current user account (saved in ~/.gitconfig).

Omitting it: Applies settings locally only to the current repository you are in (saved in .git/config). Local configuration overrides global configuration.

Question 2: Contents of .git revealed by ls -a
The .git directory contains the complete Git database and metadata tracking your project's history. Key internal contents include:

HEAD: Points to the currently checked-out branch or commit.

config: Local configuration settings specific to this repository.

objects/: The object database storing all committed file contents, commits, and tree objects.

refs/: References to branches (refs/heads/), tags (refs/tags/), and remote branches.

hooks/: Scripts executed before or after Git operations (e.g., pre-commit checks).

index (or Staging Area): Binary file tracking staged changes waiting to be committed.

Question 3: Approximate untracked file count and identifying untracked code

Untracked File Count: If a project directory contains a virtual environment (like .venv/ or node_modules/), the count can range from hundreds to thousands of files (e.g., Python libraries, dependencies, temporary binaries).

Identifying Untracked Code: Run git status. Files and folders listed under "Untracked files:" are present on your disk but not tracked by Git.

Question 4: Difference in git status after creating .gitignore
Before adding .gitignore, git status displays large folders/files (such as .venv/) under "Untracked files:". Once you list those files inside .gitignore, git status hides them entirely from untracked files and instead only shows .gitignore itself as untracked/modified.

Question 5: Why .gitignore itself should be committed rather than ignored
Committed .gitignore files ensure that every collaborator (and any new clone of the project) shares the exact same ignore rules. This prevents team members from accidentally committing junk files, temporary build artifacts, virtual environments, or operating system metadata.

Question 6: Movement of README.md across sections in git status (three-places model)
Git operates on three main areas: the Working Directory, the Staging Area (Index), and the Repository (Commit History).

Working Directory: When README.md is edited/created, git status lists it under "Changes not staged for commit" (or "Untracked files").

Staging Area: Running git add README.md moves it to "Changes to be committed" (Staging Area).

Repository: Running git commit records the staged snapshot into local Git history; README.md disappears from git status output because the working tree is clean.

Question 7: Output produced by git commit and count of changed files

Output Produced: Returns the branch name, the short commit hash, the commit message title, summary statistics on modifications (e.g., [main e756912] Lab work so far), file permissions, and mode changes.

Count of Changed Files: Displayed in the commit summary line right after execution (e.g., 3 files changed, 45 insertions(+)).

Question 8: Name and purpose of the first seven characters of a commit hash

Name: Short SHA-1 (or Short Commit Hash/Abbreviated Hash).

Purpose: Provides a unique identifier for a specific snapshot/commit while being brief enough for human reading, logging (git log --oneline), and quick command references.

Question 9: The 4 steps of the repetitive Git loop

Modify: Make edits or create new files in your working directory.

Stage: Run git add <files> to stage specific changes.

Commit: Run git commit -m "Description" to save the staged snapshot locally.

Push: Run git push to send local commits to the remote repository (e.g., GitHub).

Question 10: Special purpose and placement of README.md

Special Purpose: Serves as the primary documentation hub for project overview, setup instructions, usage guidelines, and contribution rules.

Placement: Located directly at the root directory of your repository so tools and hosting platforms can immediately locate it.

Question 11: How gh auth login eliminates future password prompts
gh auth login authenticates via Web browser OAuth or Personal Access Token (PAT) and configures a local credential helper (or stores access tokens in system keyrings). Git uses these securely stored tokens for HTTPS operations, removing the need to type your password repeatedly.

Question 12: File rendered on GitHub's front page and the reason why

File Rendered: README.md (or README.rst, README.txt) located at the root of the repository.

Reason: GitHub automatically looks for root README files and parses Markdown (.md) to display formatted visual documentation on the repository landing page for developers.

Question 13: Effect of git push on local history
Running git push does not alter or change your local commits/history. It simply uploads local commit objects to the remote branch on GitHub and updates remote tracking references (such as origin/main) to match your local main branch position.

Question 14: Distinction between a private repository vs. no repository on GitHub

Private Repository: Exists on GitHub's servers, but access is restricted to the repository owner and explicitly added collaborators. Requests return a HTTP 404 or 403 error for unauthenticated/unauthorized users.

No Repository: Does not exist on GitHub at all. Pushing or navigating to the URL always returns a "Repository not found" error regardless of authorization.