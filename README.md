
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
```


