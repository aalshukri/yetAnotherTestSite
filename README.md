# YetAnotherTestSite

This is yet another test site which I have used to try out jekyll static website generation.
This project uses github actions to build and deploy a jekyll static site to my own remote ftp server (not using github hosting on gh-pages).

## Deployment workflow

The deployment workflow follows this path

Make changes to Jekyll files on development branch.
Once any new webpages or site updates have been made, pull this branch into master.
Once master branch has been updated, this triggers a github action to build the website to 'live' branch.

When the site has been built and live branch has been updated, this triggers another github action
to deploy the site via ftp to my remote server.


## Github Actions

Build using jekyll-action 

Original github action
https://github.com/helaili/jekyll-action/

Which I forked to
https://github.com/aalshukri/jekyll-action

I am using version
aalshukri/jekyll-action@2.0.4.1

I made a minor modification to this build jekyll script.
Which was to build the jekyll static site files to 'live' branch rather than 'gh-pages' branch.
In order to do this, I needed to make a modification to the entrypoint.sh file which the variable was hard coded.


Deploy using ftp-deploy 

Orginal github action
https://github.com/SamKirkland/FTP-Deploy-Action

Which I forked to
https://github.com/aalshukri/FTP-Deploy-Action

I am using version
/aalshukri/FTP-Deploy-Action@3.1.1

My usage has the modificiation of using github secret values for 
 - ftp-server
 - ftp-username
 - ftp-password


## Trouble shoot

If you are trying to replicate this yourself, 
one of the stumblering blocks I encountered was with running github actions on branches.
As mentioned in my deployment workflow, I use the 'live' branch to keep the static website files
once built, which I then push to ftp.
In order to trigger a github workflow on a branch, you simply need to place the workflow file on that branch.
I have two in this project

branch master
.github/workflows/github-build.yml
	This file does the static site build when changes occur on master branch,
	and pushed these change to live branch


branch live
.github/workflows/github-deploy.yml
	This file pushes files to my ftp server 
	when a change occurs on live branch.




