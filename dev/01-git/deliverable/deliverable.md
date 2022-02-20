---
title: "Git Deliverable | 💙"
permalink: /dev/01-deliverable-git
layout: default
---

# Git Deliverable

*Note: This tutorial is written for those with MacOS. If you use Linux or Windows, your terminal commands may be different.*



## Overview

Your task in this deliverable is to write a simple `README.md` file that displays information about you on your GitHub page. 

![about-card](about-card.jpg)




## Repository Setup

To get started, create a new [GitHub](https://github.com/) account or log into an existing account. Click the "+" button in the top right of the page, and select "New repository". Name the repository the same name as your GitHub username, and make sure Public is selected.

![01](01.jpg)



## Clone Git Repisitory to Local Drive

Clone your repository to your local workspace by running the following commands on terminal:

```
cd Desktop
git clone https://github.com/YOURUSERNAME/YOURUSERNAME
```

Make sure to replace `YOURUSERNAME` with your actual GitHub username (eg: I would use `gracejiang`). Next, navigate into your directory using `cd YOURUSERNAME`. You can run `pwd` to check that you are in the right directory.

![02](02.jpg)

*What my terminal looks like*

Great! Your repository is now cloned to your local workspace, and you're ready to start editing it. 



## Create README.md

Create a new README.md file by running the following command on terminal:

```
touch README.md
```



Next, open your `README.md` file in [VSCode](https://code.visualstudio.com/) (install it if you don't already have it) by running the following command:

```
code .
```

Finally, add text about yourself into your `README.md` file using [Markdown](https://www.markdownguide.org/cheat-sheet/). Feel free to get creative in this step! Some cool resources to look into:

* [GitHub Stats](https://github.com/anuraghazra/github-readme-stats)



Make sure to save your file after you finish editing it.



## Push README.md to GitHub

It's time to push your changes to GitHub! To do so, run the following commands:



```
git add .
git commit -m "add about me information"
git push origin main
```



Finally, navigate to your profile to make sure your changes got pushed.

...And that's it!



## [Submit Deliverable Here](https://forms.gle/M8sGaURGmaAwGHcX7)


*Written by [Grace J.](https://gracejiang.me/)*
