---
layout: post
title: OpenKanban
---

I've relased an Open Source self-hosted Kanban written in HTML5/JS + Java as "frontend/backend". 

![_config.yml]({{ site.baseurl }}/images/openkanban.png)

Once built, just run the jar file and you will see that the web broswer will open (and a new icon will be shown on the notification bar).

With the left click of the mouse on the notification bar icon of OpenKanban, you can open a menu where you can open again the web page (or close the app).

Set the check on enable changes and save once (the button on the right).

Now that has been saved, a file called `kanbandata.json` should be in the same folder where the jar is stored.

Open that `kanbandata.json` and you will see something like this:

```json
{
    "users": [
        "USER1",
        "USER2",
        "USER3"
    ],
    "bin": [],
    "types": [
        {
            "color": "#000099",
            "name": "Generic"
        },
        {
            "color": "#996633",
            "name": "Tickets"
        },
        {
            "color": "#ff0000",
            "name": "Critical"
        }
    ],
    "lists": [
        {
            "name": "Todo",
            "tasks": []
        },
        {
            "name": "Low Priority",
            "tasks": []
        },
        {
            "name": "In Progress",
            "tasks": []
        },
        {
            "name": "Waiting Feedback",
            "tasks": []
        },
        {
            "name": "Completed",
            "tasks": []
        }
    ]
}
```

To edit the users available on the webpage, just change the `users` list, same for the type (`types` on the json) of new Task.
`lists` contains the list available on the kanban board.
`bin` will contain the removed task from the kanban.



