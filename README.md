  - uses: actions/github-script@v7
    with:
      script: |
        const fs = require('fs');

        // Combien de repos afficher, et lesquels ne jamais montrer
        const COUNT = 5;
        const HIDDEN = ['ni3ma-fer'];   // le repo de profil lui-meme

        const owner = context.repo.owner;
        const repos = await github.paginate(github.rest.repos.listForUser, {
          username: owner,
          type: 'owner',
          sort: 'pushed',      // tri par derniere activite, pas par date de creation
          direction: 'desc',
          per_page: 100,
        });

        const picked = repos
          .filter(r => !r.fork && !r.archived && !HIDDEN.includes(r.name))
          .slice(0, COUNT);

        const rows = picked
          .map(r => `| [**${r.name}**](${r.html_url}) | ${(r.description || '').replace(/\|/g, '\\|')} |`)
          .join('\n');

        const table = `| Repository | Description |\n|---|---|\n${rows}`;

        const path = 'README.md';
        const readme = fs.readFileSync(path, 'utf8');
        const updated = readme.replace(
          /<!-- PROJECTS_START -->[\s\S]*?<!-- PROJECTS_END -->/,
          `<!-- PROJECTS_START -->\n${table}\n<!-- PROJECTS_END -->`
        );

        if (updated !== readme) fs.writeFileSync(path, updated);

  - name: Commit
    run: |
      git config user.name "github-actions[bot]"
      git config user.email "41898282+github-actions[bot]@users.noreply.github.com"
      git add README.md
      git diff --quiet --staged || (git commit -m "Update recent projects" && git push)
