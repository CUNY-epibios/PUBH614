# GitHub Actions Workflow

This directory contains a single, comprehensive GitHub Actions workflow that automatically checks and validates the entire project whenever changes are made.

## Single Workflow: `ci.yml` - Comprehensive CI/CD Pipeline

**Triggers:** 
- Every push and pull request to main/develop branches
- Manual dispatch with specific workflow types
- Daily scheduled runs at 2 AM UTC

**Purpose:** Complete project validation and deployment automation

### 🎯 Key Features

#### **Smart Change Detection**
- Automatically analyzes what files changed
- Runs only relevant checks based on file types
- Optimizes CI time by skipping unnecessary checks
- Provides detailed change summaries and recommendations

#### **Comprehensive Validation**
- **R Package Checks:** Linting, testing, building on multiple R versions
- **Quarto Rendering:** Document validation and HTML generation
- **Pkgdown Building:** Complete website generation and validation
- **File Validation:** Permissions, security, formatting, and integrity checks

#### **Beta Release System** 🧪
- **Automatic beta releases** for every Pull Request
- **Downloadable R packages** for easy testing
- **Preview websites** for testing changes
- **PR comments** with testing instructions
- **Automatic cleanup** when PRs are closed

#### **Production Release Automation** 🚀
- **Automatic version bumping** on main branch pushes
- **GitHub releases** with changelog generation
- **Production deployment** to GitHub Pages
- **Manual release triggers** with version control

### 🔧 Workflow Jobs

1. **`analyze-changes`** - Detects file changes and determines what to run
2. **`r-package-checks`** - R package validation, linting, and testing
3. **`quarto-render`** - Quarto document rendering and validation
4. **`pkgdown-build`** - Website building and validation
5. **`file-validation`** - File integrity and security checks
6. **`beta-release`** - Creates beta releases for PR testing
7. **`pr-deployment`** - Deploys preview websites for PRs
8. **`production-release`** - Handles production releases and deployment
9. **`cleanup-beta-releases`** - Cleans up old beta releases
10. **`final-summary`** - Generates comprehensive results summary

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

You can manually trigger specific parts of the workflow:

1. Go to Actions tab in GitHub
2. Select "Comprehensive CI/CD Pipeline"
3. Click "Run workflow"
4. Choose workflow type:
   - `smart`: Run smart checks based on changes (default)
   - `full`: Run all checks regardless of changes
   - `r-package`: Only R package checks
   - `quarto`: Only Quarto rendering
   - `pkgdown`: Only website building
   - `files`: Only file validation
   - `beta-release`: Create beta release for specific PR
   - `release`: Create production release

### Manual Beta Release
To create a beta release for a specific PR:
1. Go to Actions tab
2. Select "Comprehensive CI/CD Pipeline"
3. Click "Run workflow"
4. Choose `beta-release` as workflow type
5. Enter the PR number you want to create a beta release for

### Manual Production Release
To create a production release:
1. Go to Actions tab
2. Select "Comprehensive CI/CD Pipeline"
3. Click "Run workflow"
4. Choose `release` as workflow type
5. Select release type: `patch`, `minor`, `major`, or `prerelease`

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
