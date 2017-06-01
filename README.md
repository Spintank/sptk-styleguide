# sptk-coding-styleguide
*The coding styleguide of Spintank*

## Table of contents
- [Syntax](#syntax)
- [Workflow](#Workflow)
- [Starting a new project](#starting-a-new-project)
- [Before release](#before-release)
- [Accessibility](#accessibility)
- [Browsers support](#browsers-support)
- [Links](#links)

## Syntax
- All in english
- Filenames and foldernames all in lowercases, no spaces, no accents.
- Think about comments, everyone could understand your code
- [See styleguides](#links)

## Workflow

### IDE
Use the IDE you prefer, we already use [Atom](https://atom.io/) and [PhpStorm](https://www.jetbrains.com/phpstorm/). The minimum is to add emmett and autocomplete plugins.

### Development

- Install [Nodejs](https://nodejs.org/en/)

- Install [NPM](https://www.npmjs.com/) (installed with [Nodejs](https://nodejs.org/en/))

- Install [Gulp](http://gulpjs.com/)

    ```bash
    npm install --global gulp-cli
    ```

- Install [Sass](http://sass-lang.com/)

    ```bash
    sudo gem install sass
    ```

- Install [Browserify](http://browserify.org/)

    ```bash
    npm install -g browserify
    ```

- Install [Homebrew](http://brew.sh/index_fr.html)

    ```bash
    /usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"
    ```

- Install [MAMP Pro](https://www.mamp.info/en/downloads/older-versions/) (the version 3, not the 4). Ask for the serial number.

### Console

- Install [Oh-my-zsh](https://github.com/robbyrussell/oh-my-zsh)

    ```bash
    sh -c "$(curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh)"
    ```

### Others
- All our projet are hosted on [GIT](https://github.com/Spintank).
- Designers uses **Sketch**, **Photoshop**, **Illustrator**. If you want, create a [zeplin](https://zeplin.io/) projet with the designer.
- Create a **"Sites" folder** on your personal folder. It contains all your sites.
- We have a **file with ftp and php accesses**. Just ask!

## Starting a new project
- Create a GIT repo (see GIT syntax)
- Clone the starterkit repo adequate in your sites folder
- Rename the starterkit folder and delete the .git file

```bash
cd Sites/nameoftherepo
git init
git remote add origin https://github.com/Spintank/nameoftherepo.git
git push -u origin master
```

That's it!

## Before release
- Make sure you have tested on a preprod version
- Check the toDolist (if possible, ask a producer doing the same)
- Test the site on W3C validator
- Test document outlines
- Disable Javascript to see if the content is accessible

## Accessibility
- Great use of headlines tags
- Avoid duplicate content. If you duplicate text for graphics effects, add aria-hidden attributes, or use pseudo-elements.
- The css class and the mixin "hide-for-viewer" hide the content for users, but not for SEO robots.
- Use <button> instead of <span> if you need an interactive element.

## Links
- [GIT styleguide](styleguide-git.md)
- [CSS styleguide](styleguide-css.md)
- [Javascript styleguide](styleguide-javascript.md)
- [Clasic starterkit](https://github.com/Spintank/sptk-starterkit)
- [Codepen](http://codepen.io/spintank/)
