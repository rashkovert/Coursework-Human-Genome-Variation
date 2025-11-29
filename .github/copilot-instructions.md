<!-- .github/copilot-instructions.md for Coursework-Human-Genome-Variation -->
# Copilot instructions — Coursework Human Genome Variation

These notes help an automated coding agent be productive in this repository. The project is a collection of teaching modules (R Markdown notebooks, data, and images). Each module is a self-contained folder named with a two-digit prefix (e.g., `02-dnm`, `03-ld`, `06-gwas`). Work is primarily in R / R Markdown; some modules call external CLI tools (PLINK).

Key patterns and where to look
- Modules: each top-level folder like `02-dnm/`, `03-ld/`, `06-gwas/` contains an `.Rmd` (or `_starter.Rmd`) and a module `README.md` that documents required data and packages.
- Rendered outputs: many modules include pre-rendered `.html` files (e.g., `04-wright_fisher/04-wright_fisher.html`) generated from the `.Rmd` files. When changing a notebook, regenerate the HTML.
- Data: small example VCF/Text/TSV files live inside each module (e.g., `06-gwas/genotypes_subset.vcf`, `02-dnm/crossovers.tsv`). Large files are gzipped (`*.vcf.gz`). Keep data edits local to module folders and update the module `README.md` when adding/removing data.
- Scripts: look for helper scripts such as `03-ld/data/data_preprocessing.R` — these contain reproducible code that R Markdown notebooks call or mirror.

Common developer workflows (how to build / test / verify)
- Install R packages required by a module inside R or via a one-liner. Example (macOS zsh):
  Rscript -e "install.packages(c('tidyverse','vcfR','ggtree','qqman'))"
- Render a module from the repo root using Rscript (non-interactive):
  Rscript -e "rmarkdown::render('02-dnm/02-dnm.Rmd', output_format='html_document')"
  This will produce the corresponding `.html` next to the `.Rmd`.
- If a module relies on PLINK (GWAS), ensure the PLINK binary is installed and on PATH. Typical PLINK usage for files in `06-gwas/`:
  plink --file 06-gwas/genotypes --assoc --out 06-gwas/plink_assoc

Project-specific conventions and expectations
- Module numbering: filenames and folders are prefixed with two-digit numbers. Keep new modules in the same naming style to preserve ordering.
- Relative paths: notebooks and scripts use relative paths to their module folder. When adding files, reference them relatively (e.g., `images/figure.png` inside the module).
- R environment: There is no unified lockfile; modules list required packages in their `README.md`. Prefer using a project-local R session (open the `.Rproj` in the module when present) or manage packages per-module.
- Outputs: When editing analysis notebooks, regenerate the HTML output so previewed content matches the source. Commit both `.Rmd` and updated `.html` if the change affects rendered output.

Integration and external dependencies
- PLINK: required for `06-gwas`. Mentioned in `06-gwas/README.md`.
- No CI or automated tests are present. Validate changes locally by rendering notebooks and checking generated HTML.

Guidance for making changes (concrete rules)
- If you edit an `.Rmd`, run `rmarkdown::render()` and include the updated `.html` alongside the `.Rmd` in the same commit.
- If you add a package dependency, update the module `README.md` under the "Software" section.
- If you add large datasets (>5–10 MB), prefer compressing (gz) and note the file in the module README; consider recommending Git LFS for very large binary data.
- Preserve image filenames and structure under `images/` to avoid breaking relative links in notebooks.

Where to look first when working in this repo
- Open the module `README.md` for the task you care about (examples: `02-dnm/README.md`, `03-ld/README.md`, `06-gwas/README.md`).
- Inspect the module `.Rmd` and any helper scripts in `data/` or `images/`.
- For GWAS tasks, review `06-gwas/genotypes_subset.vcf`, `genotypes.map`, `genotypes.ped`, and `06-gwas/README.md` for PLINK specifics.

If anything is unclear or you need more specifics (e.g., preferred commit messages, testing criteria, or which modules are actively used in grading), ask the repository owner for clarification before making large changes.

End of file.
