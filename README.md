# AutoCoder: AI-Powered DevOps Automation

**AutoCoder** is a sophisticated GitHub Composite Action designed to bridge the gap between project management and rapid software prototyping. By integrating the conversational intelligence of OpenAI's Large Language Models (LLMs) directly into the GitHub ecosystem, this tool allows developers to transform technical requirements—documented as GitHub Issues—into functional, production-ready code automatically delivered via a Pull Request.

## Technical Architecture
The core logic resides in a Bash-based engine that utilizes `curl` to communicate with the GitHub REST API and the OpenAI Chat Completions API. By leveraging the `jq` utility, the action parses issue descriptions and formats them into a prompt that demands a strictly valid JSON response. This ensures that the generated code snippets can be programmatically extracted and written to the local filesystem within the runner environment.



## How it Works
When a specific label (default: `autocoder-bot`) is applied to an issue, the action triggers a secure workflow. It handles complex tasks such as dynamic directory creation, multi-file code extraction, and automated Git configuration. Finally, the `peter-evans/create-pull-request` action stages these changes and opens a Pull Request for human review. This project serves as a practical demonstration of how autonomous agents can be harnessed to reduce developer friction and accelerate the delivery of high-quality software components.

## Usage
To use this action, set up a `.github/workflows/main.yml` file:

```yaml
on:
  issues:
    types: [opened, reopened, labeled]

jobs:
  generate_code:
    if: contains(github.event.issue.labels.*.name, 'autocoder-bot')
    runs-on: ubuntu-latest
    permissions:
      contents: write
      pull-requests: write
    steps:
      - name: Checkout repository
        uses: actions/checkout@v4
      - name: interact with ChatGPT
        uses: your-username/AutoCoder@v1
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          REPOSITORY: ${{ github.repository }}
          ISSUE_NUMBER: ${{ github.event.issue.number }}
          OPENAI_API_KEY: ${{ secrets.OPENAI_API_KEY }}
