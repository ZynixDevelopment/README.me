name: 3D Github contributions

on:
  schedule:
    - cron: "0 0 * * *" # tous les jours à minuit UTC
  workflow_dispatch:

jobs:
  build:
    runs-on: ubuntu-latest
    permissions:
      contents: write
    steps:
      - uses: actions/checkout@v4
      - uses: yoshi389111/github-profile-3d-contrib@0.7.1
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
        with:
          username: TON_USERNAME_GITHUB
      - name: Commit & push
        run: |
          git config user.name github-actions
          git config user.email github-actions@github.com
          git add -f profile-3d-contrib/*.svg
          git commit -m "generate github 3d contribution" || echo "no changes"
          git push
