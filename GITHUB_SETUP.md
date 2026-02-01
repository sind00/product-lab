# GitHub Repository Setup Instructions

---

## Option 1: Create Repo via GitHub Web Interface

1. Go to [github.com/new](https://github.com/new)
2. Repository name: `product-lab` (or whatever you prefer)
3. Description: "From $0 to $10: Building digital products"
4. Visibility: **Private** (recommended until you're ready to share)
5. Initialize with: **None** (we'll push existing files)
6. Click "Create repository"

---

## Option 2: Create Repo via GitHub CLI

If you have `gh` CLI installed:

```bash
# Navigate to the folder with all the files
cd ~/Documents/Hackathons\ \&\ Projects/github/product-lab

# Create repo and push
gh repo create product-lab --private --source=. --remote=origin --push
```

---

## Push Existing Files to GitHub

After creating the repo, run these commands in your terminal:

```bash
# Navigate to the folder containing all the files
cd ~/Documents/Hackathons\ \&\ Projects/github/product-lab

# Initialize git if not already
git init

# Add all files
git add .

# Initial commit
git commit -m "Initial commit: methodology + 5 product specs + architecture docs

- Master methodology document for $10 in 24 hours
- 5 product idea specs (makeup checker, vet tool, skincare calc, AI finder, inventory)
- Shared AI FaceTime companion architecture
- User research interview questions for vet tool

Co-Authored-By: Claude Opus 4.5 <noreply@anthropic.com>"

# Add remote (replace with your actual repo URL)
git remote add origin git@github.com:YOUR_USERNAME/product-lab.git

# Push to main branch
git push -u origin main
```

---

## Recommended .gitignore

Create a `.gitignore` file before your first commit:

```
# Dependencies
node_modules/
.pnpm-store/

# Build outputs
.next/
dist/
build/

# Environment variables
.env
.env.local
.env.*.local

# IDE
.idea/
.vscode/
*.swp
*.swo

# OS
.DS_Store
Thumbs.db

# Logs
*.log
npm-debug.log*

# Testing
coverage/

# Misc
*.bak
*.tmp
```

---

## Repository Structure After Setup

```
product-lab/
├── .gitignore
├── README.md
├── methodology.md
│
├── ideas/
│   ├── 01-makeup-expiration-checker.md
│   ├── 02-vet-decision-tool.md
│   ├── 03-korean-skincare-calculator.md
│   ├── 04-ai-tool-finder.md
│   └── 05-makeup-inventory-tracker.md
│
├── architecture/
│   └── ai-facetime-companion.md
│
└── research/
    └── vet-tool-interview-questions.md
```

---

## Future: Monorepo for Actual Code

When you start building, you might want to structure it as a monorepo:

```
product-lab/
├── docs/                    # Current specs and methodology
│   ├── methodology.md
│   ├── ideas/
│   ├── architecture/
│   └── research/
│
├── apps/                    # Actual applications
│   ├── skincare-calc/       # Korean Skincare Calculator
│   ├── makeup-checker/      # Makeup Expiration Checker
│   └── vet-tool/            # Vet Decision Tool
│
├── packages/                # Shared code
│   └── ai-facetime-core/    # Shared camera/voice/AI modules
│
└── package.json             # Monorepo config (pnpm workspaces or turborepo)
```

---

## GitHub Actions (Optional, For Later)

When you have actual code, add CI/CD:

```yaml
# .github/workflows/deploy.yml
name: Deploy

on:
  push:
    branches: [main]

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with:
          node-version: '20'
      - run: npm ci
      - run: npm run build
      - run: npm run test
      # Add Vercel deployment step here
```

---

## Quick Commands Reference

```bash
# Clone your repo to a new machine
git clone git@github.com:YOUR_USERNAME/product-lab.git

# Create a new branch for a product
git checkout -b feature/skincare-calc

# Stage and commit changes
git add .
git commit -m "Add skincare calculator MVP"

# Push branch and create PR
git push -u origin feature/skincare-calc
gh pr create --title "Add skincare calculator MVP" --body "First working version"

# Merge and delete branch
gh pr merge --squash
git branch -d feature/skincare-calc
```

---

## Notes

- Keep specs and docs in `main` branch
- Create feature branches for actual code development
- Use conventional commits if you want: `feat:`, `fix:`, `docs:`, etc.
- Consider GitHub Projects for tracking progress across products
