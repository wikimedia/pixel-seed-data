# Pixel Seed Data

This repository contains database backups that are to be used as seed data for [Pixel](https://github.com/nicholasray/pixel). Since this repo is hosted on github pages, its files can be downloaded via https://wikimedia.github.io/pixel-seed-data/name-of-file.

## Instructions

Let's say you're trying to add a new wiki page to Pixel. You would follow these steps:

1) Make sure you aren't including any unintended db changes by running `./pixel.js reset-db` before making any desired changes. This resets Pixel's database to its original state.
2) When Pixel's server is running (e.g. after running `./pixel.js reference`), visit `localhost:3000/wiki/<your-new-page>` in your browser, and click the "Create" tab to create your page, and do any other actions you wish that will affect the database.
2) In Pixel's root directory, run `npm run db:save`. This will generate a [physical backup](https://dev.mysql.com/doc/refman/8.0/en/backup-types.html#:~:text=Physical%20backup%20methods%20have%20these,only%20file%20copying%20without%20conversion) of the database Pixel uses and save it in a folder called `backups` located in Pixel's root directory.
3) Drag and drop the `tar` file located in the `backups` directory anywhere on this page (https://github.com/wikimedia/pixel-seed-data). Github will upload the file and ask you commit it to the main branch of this repo. Click "Commit changes".
4) Edit Pixel's [seedDb.sh](https://github.com/wikimedia/pixel/blob/b4af39d0be82f6f608e9fb3996b52cb9f924eabe/Dockerfile.database#L5) file with the name of this file. Commit this change and create a pull request in Pixel to merge this change into Pixel's `main` branch.
5) After the pull request has been merged, checkout the the `main` branch in Pixel and run `./pixel.js update` and then `./pixel.js reference` to rebuild the Docker database image/volume with your changes.
6) Confirm your database changes are live by visiting the server Pixel sets up at `localhost:3000`.
