# NYU Classes `Resources` Scraper

This repo contains a script to download all of the Resources for classes listed
on NYU Classes (newclasses.nyu.edu).

![A screenshot of the Resources tab on a class](screenshots/resource_screenshot.png)

### Install Dependencies:

```bash
pip install -r requirements.txt
```

### Get Class List

You can get the list of classes to scrape by going to "My Memberships" on
[newclasses.nyu.edu](newclasses.nyu.edu) and running the following Javascript in
your web browser's developer console.

![The Membership tab on the home page of newclasses.nyu.edu](screenshots/membership_screenshot.png)

You can get to the console by Right-Clicking on the webpage, then clicking
`Inspect`, then clicking the Console tab.

```javascript
JSON.stringify(
  Object.fromEntries(
    Array.from(document.querySelectorAll("[headers=worksite]")).map((x) => [
      x.children[0]?.innerText,
      x.children[0]?.href,
    ])
  )
);
```

Copy the result and save it to a text file. We recommend `classes.json` in this
folder. It should look like

```json
{
  "Class Name 1": "https://newclasses.nyu.edu/portal/site/numbers",
  "Class Name 2": "https://newclasses.nyu.edu/portal/site/differentnumbers"
}
```

spacing doesn't matter.

![Javascript command result that we copy to the clipboard to save to a file.](screenshots/command_result.png)

### Usage:

You can run the following:

```bash
python GetClassResourceData.py --user user --pass mypassword123 --json classes.json --outdir /Backup/NYUClasses
```

with

- `user`: Your NYU username
- `pass`: Your NYU password
- `json`: The path to the JSON with the classes you want to save
- `outdir`: The path to where you want to save the class folders

It will produce at `outdir` a structure like the following: the contents of the
`Resources` tab for each class in the JSON file:
![A screenshot of the folder structure produced by the script. Class name and underneath the contents.](screenshots/result_screenshot.png)
