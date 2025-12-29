# 🚀 GitHub Actions Starter Kit

> **Production-ready workflow templates for common CI/CD tasks.**  
> Stop writing YAML from scratch. Copy, paste, deploy.

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![GitHub Actions](https://img.shields.io/badge/GitHub-Actions-blue)](https://github.com/features/actions)

---

## 🎯 Why This Exists

GitHub Actions is powerful, but the learning curve is steep:

- ❌ Complex YAML syntax with subtle gotchas
- ❌ No local testing (push → wait → debug loop)
- ❌ Scattered documentation for common patterns
- ❌ Security best practices not obvious

**This kit solves that.** Battle-tested workflows you can use immediately.

---

## 📦 What's Included

| Workflow | Description | Status |
|----------|-------------|--------|
| [CI - Node.js](#nodejs-ci) | Test & lint Node/TypeScript projects | ✅ Ready |
| [CI - Python](#python-ci) | Test & lint Python projects | ✅ Ready |
| [Deploy - Vercel](#vercel-deploy) | Auto-deploy to Vercel on push | ✅ Ready |
| [Release - Semantic](#semantic-release) | Automated versioning & changelog | ✅ Ready |
| [Security - Dependabot](#dependabot) | Automated dependency updates | ✅ Ready |
| [PR - Auto Label](#auto-label) | Automatically label PRs by file path | ✅ Ready |

---

## ⚡ Quick Start

### Option 1: Copy Individual Workflows

1. Browse `.github/workflows/` in this repo
2. Copy the workflow file you need
3. Paste into your project's `.github/workflows/` directory
4. Update variables in workflow (repo name, secrets, etc.)
5. Push to GitHub

### Option 2: Clone Everything

```bash
git clone https://github.com/jamesships/github-actions-starter-kit.git
cp -r github-actions-starter-kit/.github/workflows/* your-project/.github/workflows/
```

---

## 📁 Workflow Reference

<a name="nodejs-ci"></a>
### Node.js CI (`ci-nodejs.yml`)

**Triggers:** Push to `main`, Pull Requests

**Features:**
- Multi-version Node.js testing (18, 20, 22)
- Caching for npm/yarn/pnpm
- ESLint + Prettier checks
- Test coverage reporting
- Artifact upload for reports

**Required Secrets:** None (uses defaults)

---

<a name="python-ci"></a>
### Python CI (`ci-python.yml`)

**Triggers:** Push to `main`, Pull Requests

**Features:**
- Multi-version Python testing (3.10, 3.11, 3.12)
- pip caching
- pytest with coverage
- Ruff linting
- Type checking with mypy

**Required Secrets:** None (uses defaults)

---

<a name="vercel-deploy"></a>
### Vercel Deploy (`deploy-vercel.yml`)

**Triggers:** Push to `main`

**Features:**
- Preview deploys on PRs
- Production deploy on main
- Environment URL in PR comments
- Deployment status checks

**Required Secrets:**
- `VERCEL_TOKEN`
- `VERCEL_ORG_ID`
- `VERCEL_PROJECT_ID`

---

<a name="semantic-release"></a>
### Semantic Release (`release.yml`)

**Triggers:** Push to `main`

**Features:**
- Conventional commits → automatic versioning
- Auto-generated changelog
- GitHub releases creation
- npm publishing (optional)

**Required Secrets:**
- `GITHUB_TOKEN` (automatic)
- `NPM_TOKEN` (optional, for npm publish)

---

<a name="dependabot"></a>
### Dependabot Config (`dependabot.yml`)

**Not a workflow** - Goes in `.github/dependabot.yml`

**Features:**
- Weekly dependency updates
- Grouped updates (minor/patch together)
- Auto-merge for patch updates
- Customizable per package ecosystem

---

<a name="auto-label"></a>
### Auto Label PRs (`auto-label.yml`)

**Triggers:** Pull Request opened/edited

**Features:**
- Labels based on file paths changed
- Customizable label rules
- Size labels (S/M/L/XL)

---

## 🔐 Security Best Practices

All workflows follow GitHub security recommendations:

| Practice | Implementation |
|----------|----------------|
| **Minimal permissions** | Each workflow declares only needed permissions |
| **Pinned actions** | Actions pinned to commit SHA, not tags |
| **Secret handling** | Never log secrets, use `secrets.GITHUB_TOKEN` |
| **Dependency review** | Auto-check for vulnerabilities on PRs |

---

## 💡 Tips & Gotchas

### YAML Expression Gotchas

```yaml
# ❌ WRONG - Expression needs ${{ }}
if: github.ref == 'refs/heads/main'

# ✅ CORRECT
if: ${{ github.ref == 'refs/heads/main' }}
```

### Caching Best Practices

```yaml
# Always include lockfile hash for cache key
- uses: actions/cache@v4
  with:
    path: node_modules
    key: ${{ runner.os }}-node-${{ hashFiles('**/package-lock.json') }}
```

### Local Testing

For local testing before pushing, use [act](https://github.com/nektos/act):

```bash
brew install act  # or see docs for other OS
act -l            # list available workflows
act push          # simulate push event
```

---

## 🤝 Contributing

Found a better pattern? Have a workflow not covered?

1. Fork this repo
2. Add your workflow to `.github/workflows/`
3. Update this README
4. Open a PR

---

## 📊 Roadmap

- [ ] Docker build & push workflow
- [ ] AWS/GCP deployment workflows
- [ ] Monorepo support (Turborepo/Nx)
- [ ] Mobile (React Native/Flutter)
- [ ] E2E testing (Playwright/Cypress)

---

## 📄 License

MIT License - Use freely, attribution appreciated.

---

## ⭐ Star This Repo

If these workflows save you debugging time, please star ⭐ to help others!

---

*Built by developers who were tired of YAML debugging at midnight.*
