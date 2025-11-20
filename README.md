# KiBot GitHub Action

Automatically generate KiCad fabrication outputs using [KiBot](https://github.com/INTI-CMNB/KiBot).

## What it does

- Generates Gerber files, drill files, and BOMs
- Creates 3D renders and 2D PCB images
- Produces interactive HTML documentation
- Deploys results to GitHub Pages

## Configuration

The action uses a default `config.kibot.yaml` that generates common outputs. To customize:

1. Add your own `config.kibot.yaml` to your repository root
2. The action will automatically use your config instead of the default

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

### With custom config:
```yaml
    - uses: Nautilus-UUV/nautilus-kibot-action@main
      with:
        config-path: 'config.kibot.yaml'
```

Results are uploaded as artifacts. The action also works with GitHub Pages deployment.

## GitHub Pages Setup

To deploy results to GitHub Pages:

1. **Make your repository public** (required for free GitHub Pages)
2. Go to **Settings > Pages** in your repository
3. Set **Source** to "Deploy from a branch"
4. Select **Branch: gh-pages** and **/ (root)**
5. Click **Save**

The action will automatically deploy to GitHub Pages when you push to the main branch.