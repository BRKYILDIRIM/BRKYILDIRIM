name: Generate Snake

on:
  schedule:
    # Her 6 saatte bir çalıştırılacak
    - cron: "0 */6 * * *"

  workflow_dispatch: # Bu komut, Actions sekmesinden işlemi otomatik olarak çalıştırmamıza olanak tanır

jobs:
  build:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v2

      - name: Generate the snake
        uses: Platane/snk@master
        id: snake-gif
        with:
          github_user_name: BRKYILDIRIM
          gif_out_path: dist/github-contribution-grid-snake.gif
          svg_out_path: dist/github-contribution-grid-snake.svg

      - name: Show build status
        run: git status

      - name: Push changes
        uses: ad-m/github-push-action@master
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          branch: master
          force: true

      - name: Deploy to GitHub Pages
        uses: crazy-max/ghaction-github-pages@v2.1.3
        with:
          target_branch: output
          build_dir: dist
        env:
          GITHUB_TOKEN: ${{ secrets.GITHUB_TOKEN }}
