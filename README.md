# Pixel Seed Data

This repository contains database backups that are to be used as seed data for [Pixel](https://github.com/nicholasray/pixel). Since this repo is hosted on github pages, its files can be downloaded via https://wikimedia.github.io/pixel-seed-data/name-of-file.

## Instructions

Let's say you're trying to add a new wiki page to Pixel. You would roughly follow these steps:

1) Make sure you aren't including any unintended db changes by running `./pixel.js reset-db` before making any changes. This resets Pixel's database to its original state
2) When Pixel's server is running (e.g. after running `./pixel.js reference`), visit `localhost:3000/wiki/<your-new-page>` in your browser, and click the "Create" tab to create your page, and do any other actions you wish that will affect the database.
2) In Pixel's root directory, run `npm run db:save`. This will generate a tar [physical backup](https://dev.mysql.com/doc/refman/8.0/en/backup-types.html#:~:text=Physical%20backup%20methods%20have%20these,only%20file%20copying%20without%20conversion) of the database Pixel uses and save it in a folder called `backups` located in Pixel's root directory.
3) In this repos's folder, commit the tar file (e.g. `database_2022-05-26_13-03-37-0700(PDT).tar.gz`) in this repository. Keep the same file name and **do not remove any of the previous snapshots** in your commit. They may be used by older versions of Pixel.
4) Push the commit into the main branch of this repo.
5) Edit Pixel's [seedDb.sh](https://github.com/wikimedia/pixel/blob/b4af39d0be82f6f608e9fb3996b52cb9f924eabe/Dockerfile.database#L5) with the name of this file. Commit this change and create a pull request in Pixel to merge this into Pixel's `main` branch
6) To make Pixel use the new database snapshot, you will need to run `./pixel.js clean` which recreates the Docker database image and downloads the tar file you added to this repo. This file will now be part of the new database image.
