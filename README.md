# Cake Issues Addin Website

This is the website for the Cake.Issues addins.
It's a static site generated by [Wyam](http://wyam.io).

## Contributing

Any contributions are appreciated, no matter how big or small.
The Cake Issues site consists of several different sections and each one is described below.

### Documentation

The basic documentation pages can be found under `./input/docs`.
The directory structure mirrors what's on the site.
Most pages are written in Markdown.
To add a new page, just add a new file.

### Addins

All addins are specified in individual YAML files under `./addins`.
Adding an addin here will trigger downloading its NuGet Package during site generation and will include it in the "Addins" section of the Cake Pull Request Code Analysis site.

The format of an addin file generally looks like:

```yml
Name: Team Foundation Server (TFS) & Visual Studio Team Services (VSTS) Support
NuGet: Cake.Issues.PullRequests.Tfs
Prerelease: true
Repository: https://github.com/cake-contrib/Cake.Issues.PullRequests.Tfs
Assemblies:
- "/**/Cake.Issues.PullRequests.Tfs.dll"
Author: BBT Software AG
Description: "Support for writing issues as comments to Team Foundation Server or Visual Studio Team Services pull requests."
Categories:
- Pull Request System
```

Note that the `Prerelease` flag can be omitted for non-prerelease packages and controls whether NuGet will attempt to download a prerelease version of the package when generating the site.

## Building

The site is built using Cake (of course!). There are a number of different targets depending on what you're working on and how complete you want the generated site to be.

`build -target GetAddinPackages` will download new NuGet packages for all specified addins.
These packages are used to create the "Addins" section.

`build -target GetArtifacts` will download the addin NuGet packages.

`build -target Build` will run a complete build, downloading addin NuGet packages.
Note that due to the number of addins and the complexity of generating complete API documentation, the site generation may take a while.

`build -target Preview` will run a build but *will not* download NuGet packages.
This lets you shorten the build cycle by avoiding the time to obtain those resources if you've already downloaded them, or to bypass them altogether if you're just working on something like general documentation pages.
This target will also launch a preview server to look at the generated site from a local web browser.
The URL of the generated preview site is `http://localhost:5080/`.

## Deployment

The site is deployed for every release tagged on the `master` branch.
Release numbering is in sync with numbering of the core `Cake.Issues` addins.

