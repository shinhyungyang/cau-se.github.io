# Software Engineering Group at the CAU of Kiel

## Test-run the homepage locally

### Launch the test instance

```bash
docker compose up
```

Then open http://localhost:8080 on the browser. Modifying certain files (e.g.,
\_config.yml) will force-quit the current instance.

### Shutdown the test instance

```
docker compose down
```

## Avoid GitHub Action Failures

We can run some of GitHub action jobs locally to avoid GitHub action failures.

### Checking code format

Install npm and prettier:

```bash
sudo dnf install npm
npm install prettier
```

Check what's wrong:

```bash
npx prettier . --check
```

Apply prettier suggestions:

```bash
npx prettier . --write
```

### Fix broken URLs

Install cargo, openssl-devel, and lychee. The package name for openssl-devel
differs by the deployed Linux distribution.

```bash
curl -sSf 'https://sh.rustup.rs' | sh
sudo dnf install openssl-devel
cargo install lychee
```

The most up-to-date lychee command is as followed by:

```bash
lychee --user-agent 'curl/7.54' --exclude-path README.md --exclude-path _pages/404.md --exclude-path _pages/blog.md --exclude-path _posts/2018-12-22-distill.md --exclude-path _posts/2023-04-24-videos.md --verbose --no-progress './**/*.md' './**/*.html' --exclude researchgate.net --exclude doi.org --exclude acm.org --exclude star-history.com --exclude tilburguniversity.edu --exclude app
```

If the command is modified, then update the last line in this GitHub action script:

[.github/workflows/broken-links.yml](https://github.com/cau-se/cau-se.github.io/blob/main/.github/workflows/broken-links.yml)
