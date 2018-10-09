#  DrupalCampNJ local setup

This project uses Platform.sh for hosting, Lando for local development, and Git for version control. The steps below will help you set up or connect with these tools.

## Steps to set up local site initially:  
1. Install the following on your computer: 
    1. Composer (https://getcomposer.org/)
    2. Lando (https://docs.devwithlando.io/installation/installing.html)
    3. Docker Engine (see Lando’s requirements for Docker at https://docs.devwithlando.io/installation/system-requirements.html)
    4. Platform CLI (A command line tool for interacting with the Platform.sh hosting service: https://docs.platform.sh/gettingstarted/cli.html)
    5. Git
2. NOTE: Do NOT do 'lando init' - a .lando.yml file is included
3. platform project:list to get the [project-id]  
4. platform environments -p [project-id] (to get then environments/branches)
5. platform get [project-id] [folder-name] ---- (no brackets in the real command line code - 
when you are prompted for environment, default is master. Otherwise type in environment).
6. cd [folder-name]
7. platform build (lots of “magic” happening/building here)
8. lando start
9. use url http://dcnj.lndo.site/ to go to the local site
10. install Drupal8 on the site, either through the browser or with lando drupal site:install
    1. Username: drupal8
    2. Password: drupal8
    3. Database name: drupal8
    4. Host: database (default is localhost)
11. git branch (Verify that you are not on the master branch, but instead on the branch you were assigned to work on. Do a git checkout to the branchname if you are not on the correct branch.)
12. platform db:dump --gzip -f database.sql.gz (this will download the database from git Platform.sh for the environment associated to the git branch in #11 in a gz file)
13. lando db-import database.sql.gz
14. lando drush updb
15. lando drush cr
16. lando drush uublk 1 (unblocks user 1, which is blocked by default on the live site)
17. lando drush uli 1 (gives a one time login link for user 1 on your local environment)

At this point, you should be able to log into your local environment with User 1 and test any changes you’d like to make. If not, and if you have an account on the live site, try to use your account credentials to log in. Note: if you are not an administrator on the real site, you might want to run: lando drush user-add-role administrator [your-user-name-here]
Then, at least locally, you will be an administrator.

---

## Enable Twig Debug:
1. Copy web/sites/example.settings.local.php to web/sites/default/settings.local.php
2. lando drush cr

## Steps to update local:
1. git pull (Note: may need to do ‘git clean -n’ then ‘git clean -f’ first)
2. platform build
3. platform db:dump --gzip -f database.sql.gz
4. lando db-import database.sql.gz
5. use url http://dcnj.lndo.site/ to go to the local site
6. lando drush updb
7. login with whatever login you used on the real drupalcampnj site

## To run PatternLab:
Go to root of PatternLab theme: web/themes/patternlab/  
Follow instructions in README.md

## PatternLab files to edit are here:
web/themes/patternlab/source/_patterns
