# Okay it does work.
### I was using tailwind direct classes and tried to use @apply to make it cleaner. Found out that you can't use it on cdn. So i gather my AI friends and talk to them like a retard and as a good friend them to me a professional retard two of them said just fucken give up and throw me to gulag then gigachad claude walks like a pillar man and slaps me with 10 commandments like tablet in my face when i was walking in the rain depressed with in_the_end.mp4 plays in the background. It was fucken amazing I told you.

### Steps:
1. Finish your damn static website.
2. npm init -y
Paste this on package.json and change the project name
```
  {
    "name": "your-project-name",
    "version": "1.0.0",
    "scripts": {
      "build": "tailwindcss -i ./styles.css -o ./dist/styles.css",
      "watch": "tailwindcss -i ./styles.css -o ./dist/styles.css --watch"
    },
    "devDependencies": {
      "tailwindcss": "^3.4.1"
    }
  }
```
3. npm install -D tailwindcss
4. npx tailwindcss init
5.  Paste this (Or if it matches on what it looks like then ignore)
```
  /** @type {import('tailwindcss').Config} */
  module.exports = {
    content: ["./*.{html,js}"],
    theme: {
      extend: {},
    },
    plugins: [],
  }
```
6. npx tailwindcss -i ./styles.css -o ./dist/styles.css
7. Now remove the cdn or if you dont have a cdn and used a stylesheet use this one instead
```
  <link href="./dist/styles.css" rel="stylesheet">
```
8. mkdir -p .github/workflows
9. touch .github/workflows/build.yml if it doesnt work make it manually
Paste this
```
  name: Build and Deploy
  on:
    push:
      branches: [ main ]
    pull_request:
      branches: [ main ]
  
  permissions:
    contents: write
  
  jobs:
    build:
      runs-on: ubuntu-latest
      
      steps:
      - uses: actions/checkout@v4
  
      - name: Setup Node.js
        uses: actions/setup-node@v4
        with:
          node-version: '20'
          cache: 'npm'
  
      - name: Install dependencies
        run: |
          npm ci || npm install
          npm install -g tailwindcss
  
      - name: Create dist directory
        run: mkdir -p dist
  
      - name: Build CSS
        run: |
          chmod +x ./node_modules/.bin/tailwindcss
          npx tailwindcss -i ./styles.css -o ./dist/styles.css
  
      - name: Deploy to GitHub Pages
        if: success() && github.ref == 'refs/heads/main'
        uses: peaceiris/actions-gh-pages@v3
        with:
          github_token: ${{ secrets.GITHUB_TOKEN }}
          publish_dir: .
```
10. If you see that green check in the actions move to the next step if not go to last resort part
11. GitHub repo > Settings > Pages > Build and Deployment > Source > branch is gh-pages > save > profit (Just wait like 1-5 mins it will be deployed)

Last resorts:
(Permission issues like sh: 1: tailwindcss: Permission denied / Error: Process completed with exit code 126.)
  1. Go to your repository settings
  2. Click on "Actions" under "Code and automation"
  3. Under "Workflow permissions", select "Read and write permissions"
  4. Click "Save"
