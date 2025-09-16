# GitHub Actions Workflows

This directory contains GitHub Actions workflows that automatically check and validate the entire project whenever changes are made.

## Workflows Overview

### 1. `ci.yml` - Continuous Integration
**Triggers:** Every push and pull request, plus daily at 2 AM UTC
**Purpose:** Quick checks to catch issues early
**Features:**
- Quick R package validation
- Quarto document syntax checking
- File integrity checks
- Dependency validation

### 2. `smart-checks.yml` - Intelligent Change Detection
**Triggers:** Push and pull requests to main/develop branches
**Purpose:** Runs only relevant checks based on what files changed
**Features:**
- Analyzes changed files
- Runs appropriate workflows based on file types
- Provides detailed change summaries
- Optimizes CI time by skipping unnecessary checks

### 3. `comprehensive-checks.yml` - Full Project Validation
**Triggers:** Push, pull requests, and manual dispatch
**Purpose:** Complete project validation with manual control
**Features:**
- All R package checks (linting, testing, building)
- Complete Quarto document rendering
- Full pkgdown website build
- Comprehensive file validation
- Manual trigger with specific check types

### 4. Individual Workflows

#### `r-package-checks.yml`
- R CMD check on multiple R versions
- Code linting with `lintr`
- Test coverage analysis
- Package building validation

#### `quarto-render.yml`
- Renders all Quarto documents to HTML
- Validates Quarto syntax
- Checks for rendering errors
- Uploads rendered documents as artifacts

#### `pkgdown-build.yml`
- Builds complete pkgdown website
- Validates website structure
- Deploys to GitHub Pages (main branch only)
- Uploads built site as artifacts

#### `file-validation.yml`
- File permission checks
- Large file detection
- Binary file validation
- CSV file structure validation
- Security checks for secrets
- Code formatting validation

#### `beta-release.yml` 🆕
- **Creates beta releases for PR testing**
- Builds R package and pkgdown site
- Uploads package as downloadable artifact
- Comments on PR with testing instructions
- Updates release when PR is updated
- Cleans up when PR is closed

#### `pr-deployment.yml` 🆕
- **Creates preview website for PRs**
- Deploys pkgdown site to GitHub Pages
- Creates unique URL for each PR
- Comments on PR with preview link
- Perfect for testing website changes

#### `release.yml` 🆕
- **Automated releases on main branch**
- Bumps version automatically
- Creates GitHub releases with changelog
- Deploys to production GitHub Pages
- Supports manual release triggers

## How It Works

### Automatic Triggers
- **Every push/PR:** `ci.yml` runs quick checks
- **Main/develop branches:** `smart-checks.yml` runs intelligent checks
- **Manual:** `comprehensive-checks.yml` can be triggered manually

### Change Detection
The workflows use `dorny/paths-filter` to detect what types of files changed:
- **R files:** `.R`, `DESCRIPTION`, `NAMESPACE`, `man/`
- **Quarto files:** `vignettes/*.qmd`
- **Data files:** `datasets/`
- **Config files:** `_pkgdown.yml`, `pkgdown/`, `.github/`
- **Docs files:** `docs/`, `vignettes/*.html`

### Smart Execution
- Only runs relevant checks based on changed files
- Saves CI time and resources
- Provides clear feedback on what was checked

## Beta Release Testing 🧪

### Automatic Beta Releases
When you create a Pull Request, the system automatically:
1. **Creates a beta release** with your changes
2. **Builds the R package** and pkgdown site
3. **Comments on the PR** with download links
4. **Updates the release** when you push new commits
5. **Cleans up** when the PR is closed

### Testing Beta Releases
1. Open any Pull Request
2. Wait for the "Beta Release Created!" comment
3. Download the `PUBH614_*.tar.gz` file
4. Install in R: `install.packages("PUBH614_*.tar.gz", repos = NULL, type = "source")`
5. Test your changes and report issues in PR comments

### Preview Websites
For PRs with website changes:
1. Look for the "Preview Site Available!" comment
2. Click the preview URL to test the website
3. Navigate through all sections to verify changes
4. Test interactive R code execution

## Manual Workflow Dispatch

You can manually trigger the comprehensive checks with different options:

1. Go to Actions tab in GitHub
2. Select "Comprehensive Project Checks"
3. Click "Run workflow"
4. Choose check type:
   - `all`: Run all checks
   - `r-package`: Only R package checks
   - `quarto`: Only Quarto rendering
   - `pkgdown`: Only website building
   - `files`: Only file validation

### Manual Beta Release
You can also create a beta release manually:
1. Go to Actions tab
2. Select "Beta Release for PR Testing"
3. Click "Run workflow"
4. Enter the PR number you want to create a beta release for

## Artifacts

Several workflows create artifacts that you can download:
- **rendered-quarto-docs:** All rendered HTML files
- **pkgdown-site:** Complete built website
- **r-check-results:** R package check results

## Monitoring

- Check the Actions tab for workflow status
- Review the summary reports in each workflow run
- Download artifacts if needed for debugging
- Set up notifications for failed workflows

## Customization

To modify the workflows:
1. Edit the `.yml` files in this directory
2. Adjust triggers, steps, or conditions as needed
3. Test changes in a feature branch first
4. The workflows will automatically run on your changes

## Troubleshooting

### Common Issues
- **R package check failures:** Check DESCRIPTION file and dependencies
- **Quarto rendering errors:** Validate .qmd syntax and dependencies
- **Pkgdown build failures:** Check _pkgdown.yml configuration
- **File validation warnings:** Review file permissions and formats

### Getting Help
- Check workflow logs for detailed error messages
- Review the change analysis in smart-checks workflow
- Download artifacts to inspect generated files
- Open an issue if workflows are not working as expected
