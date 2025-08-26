name: Generate Snake

on:
  schedule:
    # jalan setiap jam 07:00 WIB
    - cron: "0 0 * * *"
  workflow_dispatch:

permissions:
  contents: write

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4

      # Generate SVG + GIF
      - uses: Platane/snk@v3
        with:
          github_user_name: erycaaaaa   # username kamu
          outputs: |
            dist/github-snake.svg
            dist/github-snake-dark.svg?palette=github-dark
            dist/github-snake.gif

      # Deploy hasil ke branch "output"
      - name: Deploy to output branch
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: ./dist
          publish_branch: output
