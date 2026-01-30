# Publishing Guide

Step-by-step guide to publish UI/UX Master to GitHub and ClawdHub.

## Prerequisites

- Git installed
- GitHub account
- ClawdHub account ([clawdhub.com](https://clawdhub.com))
- Clawdbot CLI installed

## Step 1: Initialize Git Repository

```bash
cd /Users/krunalbhalala/clawd/skills/ui-ux-master

# Initialize git (if not already done)
git init

# Add all files
git add .

# First commit
git commit -m "Initial release: UI/UX Master v1.0.0"
```

## Step 2: Create GitHub Repository

### Option A: Via GitHub Website

1. Go to [github.com/new](https://github.com/new)
2. Repository name: `ui-ux-master`
3. Description: "Master UI/UX design skill for Apple platforms & modern web"
4. Visibility: **Public**
5. **Do NOT** initialize with README (we have one)
6. Click "Create repository"

### Option B: Via GitHub CLI

```bash
# Install GitHub CLI if needed
brew install gh

# Authenticate
gh auth login

# Create repository
gh repo create ui-ux-master --public --description "Master UI/UX design skill for Apple platforms & modern web" --source=.

# Push code
git push -u origin main
```

## Step 3: Push to GitHub

```bash
# Add remote (replace kdbhalala)
git remote add origin https://github.com/kdbhalala/ui-ux-master.git

# Push to main branch
git branch -M main
git push -u origin main
```

## Step 4: Create GitHub Release

### Via GitHub Website

1. Go to your repository
2. Click "Releases" → "Create a new release"
3. Tag version: `v1.0.0`
4. Release title: `UI/UX Master v1.0.0 - Initial Release`
5. Description:
   ```markdown
   ## 🎨 UI/UX Master v1.0.0

   Master UI/UX design skill combining Apple HIG, modern web design, and universal principles.

   ### Features
   - Complete Apple HIG (iOS, macOS, watchOS)
   - Modern web design patterns
   - oklch color systems
   - Accessibility (WCAG AA/AAA)
   - Dark mode implementation
   - 16 reference guides
   - Code examples (SwiftUI, CSS, HTML)

   ### Installation
   ```bash
   clawdhub install ui-ux-master
   ```

   ### Documentation
   - [README](README.md)
   - [SKILL.md](SKILL.md)
   - [Contributing](CONTRIBUTING.md)

   ### What's Included
   - 15KB main guide
   - 16 reference files (~35KB)
   - Design checklists
   - Quick decision guides
   ```
6. Attach `ui-ux-master.skill` file (packaged skill)
7. Click "Publish release"

### Via GitHub CLI

```bash
# Create release with packaged skill
gh release create v1.0.0 \
  ui-ux-master.skill \
  --title "UI/UX Master v1.0.0 - Initial Release" \
  --notes "Master UI/UX design skill with Apple HIG, modern web patterns, and universal principles."
```

## Step 5: Publish to ClawdHub

### Prepare Package

```bash
# Ensure you're in the skill directory
cd /Users/krunalbhalala/clawd/skills/ui-ux-master

# Package the skill
python3 /Users/krunalbhalala/.nvm/versions/node/v20.20.0/lib/node_modules/clawdbot/skills/skill-creator/scripts/package_skill.py .

# Verify the .skill file was created
ls -lh ui-ux-master.skill
```

### Publish via ClawdHub CLI

```bash
# Install ClawdHub CLI (if not already)
npm install -g clawdhub

# Login to ClawdHub
clawdhub login

# Publish the skill
clawdhub publish ./ui-ux-master.skill

# Or publish from directory
clawdhub publish .
```

### Publish via ClawdHub Website

1. Go to [clawdhub.com/publish](https://clawdhub.com/publish)
2. Click "Upload Skill"
3. Select `ui-ux-master.skill` file
4. Fill in metadata:
   - **Name:** UI/UX Master
   - **Description:** Master UI/UX design skill combining Apple HIG, modern web design, and universal principles
   - **Tags:** ui, ux, design, apple, ios, macos, web, accessibility
   - **Category:** Design
   - **License:** MIT
   - **GitHub URL:** https://github.com/kdbhalala/ui-ux-master
5. Upload screenshots (optional)
6. Click "Publish"

## Step 6: Update package.json

Update the repository URL in package.json:

```json
{
  "repository": {
    "type": "git",
    "url": "https://github.com/kdbhalala/ui-ux-master.git"
  },
  "homepage": "https://github.com/kdbhalala/ui-ux-master",
  "bugs": {
    "url": "https://github.com/kdbhalala/ui-ux-master/issues"
  }
}
```

Commit and push:

```bash
git add package.json
git commit -m "Update: Repository URLs"
git push
```

## Step 7: Update README.md

Update GitHub links in README.md:

- Replace `kdbhalala` with your actual GitHub username
- Update badge URLs
- Update support links

```bash
git add README.md
git commit -m "Update: GitHub links"
git push
```

## Step 8: Verify Installation

Test that the skill can be installed:

```bash
# Via ClawdHub
clawdhub install ui-ux-master

# Via GitHub
clawdhub install kdbhalala/ui-ux-master

# Verify it's installed
clawdbot skill list
```

## Step 9: Promote Your Skill

### Add Topics to GitHub Repository

1. Go to your GitHub repository
2. Click the gear icon next to "About"
3. Add topics:
   - `agent-skills`
   - `ui-design`
   - `ux-design`
   - `apple-hig`
   - `web-design`
   - `accessibility`
   - `clawdbot`
   - `design-system`

### Share on Social Media

```
🎨 Just published UI/UX Master - a comprehensive design skill for @clawdbot!

✅ Apple HIG (iOS, macOS, watchOS)
✅ Modern web design
✅ Accessibility (WCAG)
✅ Dark mode
✅ 50+ KB of design guidance

Install: clawdhub install ui-ux-master
GitHub: https://github.com/kdbhalala/ui-ux-master

#UIDesign #UXDesign #AgentSkills
```

### Submit to Communities

- [Agent Skills Showcase](https://agentskills.io)
- [ClawdHub Featured](https://clawdhub.com/featured)
- Designer News
- Product Hunt (optional)

## Maintenance

### Updating the Skill

1. Make changes
2. Update version in package.json and SKILL.md frontmatter
3. Update CHANGELOG.md
4. Commit and push
5. Create new GitHub release
6. Republish to ClawdHub

```bash
# Update version
git add .
git commit -m "Release: v1.1.0"
git tag v1.1.0
git push origin main --tags

# Create release
gh release create v1.1.0 ui-ux-master.skill

# Republish to ClawdHub
clawdhub publish .
```

## Troubleshooting

### Skill Validation Fails
```bash
# Run validation manually
python3 [path-to-validator]/quick_validate.py .
```

### Package Size Too Large
- Move large files to references/
- Use external links for images
- Compress examples

### ClawdHub Publish Fails
- Ensure you're logged in: `clawdhub login`
- Check internet connection
- Verify .skill file is valid
- Contact ClawdHub support

## Support

- **GitHub Issues:** Report bugs and request features
- **GitHub Discussions:** Ask questions and share ideas
- **ClawdHub:** Contact via clawdhub.com/support

---

Good luck with your skill! 🚀
