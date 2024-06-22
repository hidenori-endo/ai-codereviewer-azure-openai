# AI Code Reviewer

This is a fork of https://github.com/freeedcom/ai-codereviewer
Modified Using Azure OpenAI.

## Setup

1. Deploy Azure OpenAI model

2. Add the Azure OpenAI API key as a GitHub Secret in your repository with the name `AZURE_OPENAI_API_KEY`.

3. Create a `.github/workflows/main.yml` file in your repository and add the following content:

```yaml
name: AI Code Reviewer

on:
  pull_request:
    types:
      - opened
      - synchronize
permissions: write-all
jobs:
  review:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout Repo
        uses: actions/checkout@v3

      - name: AI Code Reviewer
        uses: hidenori-endo/ai-code-reviewer-azure-openai@main
        with:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }} # The GITHUB_TOKEN is there by default so you just need to keep it like it is and not necessarily need to add it as secret as it will throw an error. [More Details](https://docs.github.com/en/actions/security-guides/automatic-token-authentication#about-the-github_token-secret)
          AZURE_OPENAI_ENDPOINT: ${{ secrets.AZURE_OPENAI_ENDPOINT }}
          AZURE_OPENAI_API_KEY: ${{ secrets.AZURE_OPENAI_API_KEY }}
          AZURE_OPENAI_DEPLOYMENT_ID: ${{ secrets.AZURE_OPENAI_API_KEY }}
          RESPONSE_LANG_PROMPT: "please answer in English" # Optional: You can specify answer language in this prompt
          exclude: "**/*.json, **/*.md" # Optional: exclude patterns separated by commas
```

## License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for more information.
