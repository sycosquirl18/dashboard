# Repository Instructions

## GitHub Agentic Workflow Authentication

This repository is owned by `sycosquirl18`, but GitHub Agentic Workflows must use the `noencke` Copilot subscription through the repository Actions secret named `COPILOT_GITHUB_TOKEN`.

For every Copilot-engine workflow under `.github/workflows/*.md`:

- Use the GitHub Copilot engine, either explicitly with `engine: copilot` or through the default engine.
- Use PAT authentication backed by `secrets.COPILOT_GITHUB_TOKEN`.
- Do not grant `permissions.copilot-requests: write`; omit that permission or set it to `none`.
- Do not enable the legacy `features.copilot-requests: true` setting, which migrates to `permissions.copilot-requests: write`.
- Do not select a non-GitHub `engine.model-provider` or configure Copilot BYOK through `COPILOT_PROVIDER_BASE_URL`, `COPILOT_PROVIDER_API_KEY`, or `COPILOT_PROVIDER_BEARER_TOKEN` in `engine.env`.
- Do not override `COPILOT_GITHUB_TOKEN` in `engine.env`; let gh-aw inject `${{ secrets.COPILOT_GITHUB_TOKEN }}`.
- When `gh aw add-wizard` asks for the Copilot authentication method, choose the PAT option, not organization billing or `copilot-requests`.
- Ignore compiler tips that recommend enabling `copilot-requests: write` for organization billing.

After changing an agentic workflow, run `gh aw compile --validate` and inspect the generated `.lock.yml` file.

The `Execute GitHub Copilot CLI` step must contain `COPILOT_GITHUB_TOKEN: ${{ secrets.COPILOT_GITHUB_TOKEN }}` and must not contain `COPILOT_GITHUB_TOKEN: ${{ github.token }}` or `S2STOKENS: "true"`.