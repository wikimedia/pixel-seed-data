# Pixel Seed Data

This repository contains database backups that are to be used as seed data for [Pixel](https://github.com/nicholasray/pixel). Since this repo is hosted on github pages, its files can be downloaded via https://wikimedia.github.io/pixel-seed-data/name-of-file.

## Instructions

Let's say you're trying to add a new wiki page to Pixel. You would follow these steps:

1) Make sure you are on on the latest version of Pixel (including the latest database changes) and have a fresh copy of the database seed data by running `./pixel.js update` (from Pixel's root directory and after you `git checkout` the `main` branch) before making any desired changes.
2) Run `./pixel.js reference` to pull the latest code changes from MediaWiki. Then visit `localhost:3000/wiki/<your-new-page>` in your browser, and click the "Create" tab to create your page, etc. to do any other actions you wish that will affect the database.
3) In Pixel's root directory, run `npm run db:save`. This will generate a [physical backup](https://dev.mysql.com/doc/refman/8.0/en/backup-types.html#:~:text=Physical%20backup%20methods%20have%20these,only%20file%20copying%20without%20conversion) of the database Pixel uses and will save it in a folder called `backups` located in Pixel's root directory.
4) Drag and drop the `tar` file located in the `backups` directory anywhere on the page at https://github.com/wikimedia/pixel-seed-data. Github will upload the file and ask you to commit it to the main branch of this repo. Click "Commit changes".
5) IMPORTANT: Wait for the [CI Job](https://github.com/wikimedia/pixel-seed-data/actions) to pass before proceeding to the next step. It can take awhile (5 - 10 minutes) before the file is available to be downloaded.
6) Edit Pixel's [Dockerfile.database](https://github.com/wikimedia/pixel/blob/b4af39d0be82f6f608e9fb3996b52cb9f924eabe/Dockerfile.database#L5) file with the name of the `tar` file. Commit this change and create a pull request in Pixel to merge this change into Pixel's `main` branch.
7) After the pull request has been merged, locally checkout the `main` branch in Pixel and run `./pixel.js update` to rebuild the Docker database image/volume with your changes.
8) Confirm your database changes are live by running `./pixel.js reference` and visiting the server Pixel sets up at `localhost:3000`.
9) Pixel runs hourly reports via a cron job at [https://pixel.wmcloud.org/](https://pixel.wmcloud.org/). On the next run, Pixel will automatically pull down the latest database image without any manual intervention if everything is working correctly.
