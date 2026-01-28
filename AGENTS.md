# AGENTS.md

This document provides guidance for AI agents working on the HSRTReport LaTeX Template repository.

## Project Overview

HSRTReport is a professional LaTeX document class for academic papers and theses at the University of Applied Sciences Reutlingen (Hochschule Reutlingen). It is based on KOMA-Script's `scrbook` class and provides a consistent, professional layout with minimal configuration.

## Repository Structure

```
<repo-root>/
├── src/                    # Document Source Code
│   ├── Chapters/           # Chapter content files
│   ├── HSRTReport/         # Document class (git submodule)
│   ├── Main.tex            # Main document entry point
│   ├── Main.bib            # Bibliography file (BibTeX format)
│   ├── Preamble.tex        # Custom packages and commands
│   ├── Metadata.tex        # Title page configuration
│   ├── Glossary.tex        # Glossary definitions
│   └── .latexmkrc          # LaTeXmk configuration
├── build/                  # Output directory (generated)
├── .github/
│   └── workflows/          # CI/CD pipelines
│       ├── release.yml     # Release workflow (on version tags)
│       └── continuous-release.yml  # Continuous build (on push to main)
├── Makefile                # Build automation
├── Tectonic.toml           # Tectonic project configuration
├── docker-compose.yml      # Docker build configuration
└── README.md               # Project documentation
```

## Technology Stack

- **LaTeX Engine**: Tectonic (XeLaTeX-based, self-contained)
- **Document Class**: Custom `HSRTReport` class (based on KOMA-Script `scrbook`)
- **Bibliography**: BibLaTeX with BibTeX backend
- **Build System**: Make, Tectonic, or Docker
- **CI/CD**: GitHub Actions
- **License**: CC BY-SA 4.0

## Building the Project

### Using Tectonic (Recommended)

```bash
# Build the PDF
tectonic -X build

# Or using Make
make compile
```

### Using Docker

```bash
make docker-build
```

### Prerequisites

- **Tectonic**: Modern TeX/LaTeX engine
- **GNU Make**: For build automation (optional)
- **Docker**: Alternative build environment (optional)

## Key Files for Modification

### Content Editing

- `src/Chapters/` - Add or modify chapter content here
- `src/Main.tex` - Add chapter includes and document structure
- `src/Main.bib` - Bibliography entries
- `src/Glossary.tex` - Glossary and acronym definitions
- `src/Metadata.tex` - Title page and document metadata

### Template Customization

- `src/Preamble.tex` - Custom packages and commands
- `src/HSRTReport/` - Document class source (submodule)

### Build Configuration

- `Makefile` - Build targets and automation
- `Tectonic.toml` - Tectonic build settings
- `docker-compose.yml` - Docker build configuration

## Document Class Options

The HSRTReport class accepts these options in `src/Main.tex`:

| Option | Description |
|--------|-------------|
| `paper=a4` | Paper size (a4, letter, etc.) |
| `fontsize=11pt` | Base font size (10pt, 11pt, 12pt) |
| `oneside`/`twoside` | Single or double-sided layout |
| `onecolumn`/`twocolumn` | Single or double column layout |
| `DIV=14` | Type area calculation factor |
| `variant=meti` | Report variant (meti, mki, huc) |
| `footerlogos` | Include logos in footer |
| `toc` | Include table of contents |
| `bibliography` | Include bibliography |
| `glossary` | Include glossary (requires manual build) |
| `acronyms` | Include acronyms (requires manual build) |

## CI/CD Workflows

### Release Workflow (`release.yml`)
- Triggers on version tags (e.g., `v1.0.0`, `release-2024-10`)
- Creates GitHub release with compiled PDF
- Generates changelog and source archive

### Continuous Workflow (`continuous-release.yml`)
- Triggers on push to `main` branch
- Creates continuous release with compiled PDF

## Common Tasks

### Adding a New Chapter

1. Create a new `.tex` file in `src/Chapters/`
2. Add `\input{Chapters/your_chapter}` in `src/Main.tex`

### Adding Bibliography Entries

Add entries to `src/Main.bib` in BibTeX format:

```bibtex
@article{key,
  author = {Author Name},
  title = {Article Title},
  journal = {Journal Name},
  year = {2024}
}
```

### Adding Custom Packages

Add to `src/Preamble.tex`:

```latex
\usepackage{packagename}
```

### Modifying Title Page

Edit `src/Metadata.tex` using:

```latex
\AddTitlePageDataLine{Field Name}{Field Content}
\AddTitlePageDataSpace{5pt}
```

## Known Limitations

1. **Glossary/Acronyms**: Won't work with Tectonic (requires `makeindex`)
2. **SVG Images**: Not supported (convert to PDF or PNG)
3. **Shell Escape**: Limited support in Tectonic

## Testing Changes

After making changes, build the document to verify:

```bash
make compile
# Or
tectonic -X build
```

The compiled PDF will be in `build/Main/Main.pdf`.

## Code Style Guidelines

### LaTeX Files

- Use consistent indentation (2 spaces recommended)
- Add comments for complex macros
- Group related commands with section comments
- Use descriptive file names for chapters

### File Organization

- Keep chapters in `src/Chapters/`
- Place custom commands in `src/Preamble.tex`
- Document class modifications go in `src/HSRTReport/`

## Contact

For questions or issues:
- Open a GitHub issue
- Contact: frederik@beimgraben.net
