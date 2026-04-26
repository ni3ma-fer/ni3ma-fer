name: Update README Projects

on:
  schedule:
    - cron: '0 3 * * *'
  push:
    branches: [main]
  workflow_dispatch:

jobs:
  update-readme:
    runs-on: ubuntu-latest
    permissions:
      contents: write

    steps:
      - uses: actions/checkout@v4

      - name: Set up Python
        uses: actions/setup-python@v5
        with:
          python-version: '3.11'

      - name: Install dependencies
        run: pip install requests

      - name: Fetch repos and update README
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
          GITHUB_USERNAME: ni3ma-fer
        run: |
          python3 << 'EOF'
          import requests
          import re
          import os

          username = os.environ["GITHUB_USERNAME"]
          token = os.environ["GITHUB_TOKEN"]

          headers = {"Authorization": f"token {token}"}
          url = f"https://api.github.com/users/{username}/repos?sort=updated&per_page=10&type=public"
          repos = requests.get(url, headers=headers).json()

          rows = []
          for repo in repos:
              if repo.get("fork") or repo["name"] == username:
                  continue
              name = repo["name"]
              desc = repo.get("description") or "—"
              stars = repo.get("stargazers_count", 0)
              link = repo["html_url"]
              star_str = f"⭐ {stars}" if stars > 0 else "⭐"
              rows.append(f"| [**{name}**]({link}) | {desc} | {star_str} |")

          table = "| Repository | Description | Stars |\n|---|---|---|\n"
          table += "\n".join(rows[:8])

          with open("README.md", "r") as f:
              content = f.read()

          new_content = re.sub(
              r"<!-- PROJECTS_START -->.*?<!-- PROJECTS_END -->",
              f"<!-- PROJECTS_START -->\n{table}\n<!-- PROJECTS_END -->",
              content,
              flags=re.DOTALL
          )

          with open("README.md", "w") as f:
              f.write(new_content)

          print("README updated successfully.")
          EOF

      - name: Commit changes
        run: |
          git config --local user.email "action@github.com"
          git config --local user.name "GitHub Action"
          git diff --quiet && echo "No changes" || (git add README.md && git commit -m "chore: auto-update projects" && git push)
