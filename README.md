# sptk-coding-styleguide
*The coding styleguide of Spintank*

## Table of contents
- [Syntax](#syntax)
- [Workflow](#Workflow)
- [Self-organization](#self-organization)
- [Starting a new project](#starting-a-new-project)
- [Before release](#before-release)
- [Accessibility](#accessibility)
- [Browsers support](#browsers-support)
- [Links](#links)

## Syntax
- All in english
- Filenames and foldernames all in lowercases, no spaces, no accents.
- Think about comments, everyone could understand your code
- See GIT styleguide
- See HTML styleguide
- See CSS/SCSS styleguide
- See JS styleguide
- See PHP styleguide

## Workflow
- Use the IDE you prefer, we already use Atom and PhpStorm. The minimum is to add emmett and autocomplete plugins.
- Designers uses Sketch, Photoshop, Illustrator. If you want, create a zeplin projet with the designer.
- All our projet are hosted on Git.
- Install Nodejs, npm, then gulp, sass, browserify globally. All our projects works with its.
- Install oh-my-zsh for your console. (please make sure you know how to navigate with the console!)
- Install homebrew.
- Install a FTP client.
- Install MAMP Pro (the version 3, not the 4). Ask for the serial number.
- Create a "Sites" folder on your personal folder. It contains all your sites.
- We have a file with ftp and php accesses. Just ask!

## Self-organization
Pense toujours à trier/réorganiser tes dossiers, tes fichiers, ton code. Ne laisse rien trainer sur le bureau. Toujours pusher sur Git en partant de l'agence.

## Starting a new project
- Create a GIT repo (see GIT syntax)
- Clone the starterkit repo adequate in your sites folder :
-- Raw html starterkit
-- Wordpress starterkit
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
- 
## Links
- Codepen
- GIT styleguide
- HTML styleguide
- CSS/SCSS styleguide
- JS styleguide
- PHP styleguide

