# AutoCoder

AutoCoder is an automated development tool designed to streamline the coding process by integrating GitHub Actions with OpenAI's ChatGPT API. This project serves as a centralized hub for configuration files and custom scripts that facilitate automated code reviews, suggestions, and script generation directly within the GitHub ecosystem.

By leveraging Bash scripting and CI/CD workflows, AutoCoder aims to reduce manual overhead for developers. The repository is structured to handle various automation tasks, starting with core configuration in the `.github/workflows` directory and extending to logic-heavy operations within the `scripts/` folder. This project is a practical exploration of how Large Language Models can be harnessed to improve software development lifecycles.

## How to use the AutoCoder Action

To integrate AutoCoder into your own project, create a `.github/workflows/autocoder.yml` file:

```yaml
on:
  issues:
    types: [labeled]

jobs:
  autocode:
    if: github.event.label.name == 'autocoder-bot'
    runs-on: ubuntu-latest
    permissions:
      contents: write
      pull-requests: write
    steps:
      - uses: albajoseph/AutoCoder@v1
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          REPOSITORY: ${{ github.repository }}
          ISSUE_NUMBER: ${{ github.event.issue.number }}
          OPENAI_API_KEY: ${{ secrets.OPENAI_API_KEY }}

---

### 3. Final Deployment Steps
1.  **Commit and Push**: Add `action.yml` and the updated `README.md` to your repo.
2.  **Tag a Release**: In your GitHub repository, go to **Releases** > **Create a new release**. Tag it as `v1` (or `v1.0.0`). This allows users to reference your action as `albajoseph/AutoCoder@v1`.
3.  **Permissions Check**: The script still relies on `jq` and specific arguments, so ensuring those are defined in the `runs` section of `action.yml` is vital for it to be "standalone".

Once you have pushed the metadata file and updated the documentation, provide your repository URL in the IDE and click **Check**. Congratulations on completing the project!
