# KiBot GitHub Action

Automatically generate KiCad fabrication outputs using [KiBot](https://github.com/INTI-CMNB/KiBot).

## What it does

- Generates Gerber files, drill files, and BOMs
- Creates 3D renders and 2D PCB images
- Produces interactive HTML documentation
- Deploys results to GitHub Pages

## Setup

1. Add your own `config.kibot.yaml` to your repository root, otherwise action defaults to [this one](https://github.com/Nautilus-UUV/nautilus-kibot-action/blob/main/config.kibot.yaml).
2. Enable GitHub Pages:
  1. **Make your repository public** (required for free GitHub Pages)
  2. Go to **Settings > Pages** in your repository
  3. Set **Source** to "Deploy from a branch"
  4. Run workflow
  5. Select **Branch: gh-pages** and **/ (root)**
  6. Click **Save**

## Example Workflow

Add this workflow to `.github/workflows/kibot.yml`:

```yaml
name: KiBot
on:
  push:
    paths:
      - '**.kicad_sch'
      - '**.kicad_pcb'
      - 'config.kibot.yaml'
  workflow_dispatch:

jobs:
  pcb:
    runs-on: ubuntu-latest
    container: ghcr.io/inti-cmnb/kicad9_auto_full:latest
    steps:
    - uses: actions/checkout@v4
    - uses: Nautilus-UUV/nautilus-kibot-action@main
```

### Customise options:
```yaml
    - uses: Nautilus-UUV/nautilus-kibot-action@main
      with:
        config-path: 'config.kibot.yaml' # defaults to ''
        deploy-to-pages: 'false' # defaults to 'true'
        pages-branch: 'website' # defaults to 'gh-pages'
```

Results are uploaded as artifacts and automatically deployed to GitHub Pages by default.
