# pixel-seed-data

This repository contains database snapshots that are to be used as seed data for [Pixel](https://github.com/nicholasray/pixel). Since this repo is hosted on github pages, its files can be downloaded via https://nicholasray.github.io/pixel-seed-data/<name-of-file>.

## Instructions

Let's say you're trying to add a new wiki page to Pixel. You would roughly follow these steps:

1) When Pixel's server is running (e.g. after running `./pixel.js test`), visit `localhost:3000/wiki/<your-new-page>` in your browser, and click the "Create" tab, etc.
2) In Pixel's root directory, run `npm run db:save`. This will generate a tar snapshot of the database Pixel uses and save it in a folder called `backups` located in Pixel's root directory.
3) In this repos's folder, create a new branch locally and commit the tar file (e.g. `database_2022-05-26_13-03-37-0700(PDT).tar.gz`) in this repository. Keep the same file name and **do not remove any of the previous snapshots** in your commit. They may be used by older versions of Pixel.
4) Push the commit and open a pull request to merge the commit into the main branch of this repo.
5) Edit Pixel's [seedDb.sh](https://github.com/nicholasray/pixel/blob/63d5b2947be13e828a293bc7c7f9748101d54904/src/seedDb.sh#L3) with the name of this file.
6) Create a pull request in Pixel with the change in the previous step.
