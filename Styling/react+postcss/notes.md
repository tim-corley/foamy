# Customizing React Project

## to leverage PostCSS

### create-react-app

1. create a fork of create-react-app project
2. clone forked project to local machine / project dir
3. copy the **react-scripts** folder from the **packages** folder into a new folder (ex.: _custom-react-scripts_)

```bash
/home/tim/GitHub/tim-corley/create-react-app/packages

➜  packages git:(master) cp -r react-scripts ../../custom-react-scripts
```

**be sure to copy the new cra-template folder contents into custom-react-scripts/template**

4. update `package.json` in custom-react-scripts

```json
{
  "name": "custom-react-scripts",
  ...
}
```

5. initialize folder and create new repo (push changes)

```bash
/home/tim/GitHub/tim-corley/custom-react-scripts

➜  custom-react-scripts git init
Initialized empty Git repository in /home/tim/GitHub/tim-corley/custom-react-scripts/.git/
➜  custom-react-scripts git:(master) ✗ gh repo create -d "using PostCSS in React"
✓ Created repository tim-corley/custom-react-scripts on GitHub
✓ Added remote https://github.com/tim-corley/custom-react-scripts.git
➜  custom-react-scripts git:(master) ✗ git add .
➜  custom-react-scripts git:(master) ✗ git commit -m "initial commit"
➜  custom-react-scripts git:(master) ✗ git push -u origin master
```

6. create a new react application (with `create-react-app`) with the custom script

```bash
➜  tim-corley npx create-react-app custom-application --scripts-version git+ssh://git@github.com:tim-corley/custom-react-scripts.git
```
