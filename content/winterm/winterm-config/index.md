---
title: "Windows Terminalの設定"
date: 2025-02-14T15:55:23+09:00
---

## キーバインド

Ctrl+Tabでタブの切り替えではなくペインの切り替えをしたいので`settings.json`に以下を追記しています。

``` json
    "actions": 
    [
        {
            "command": 
            {
                "action": "moveFocus",
                "direction": "nextInOrder"
            },
            "id": "User.moveFocus.D7681B66",
            "keys": "ctrl+tab"
        },
        {
            "command": 
            {
                "action": "moveFocus",
                "direction": "previousInOrder"
            },
            "id": "User.moveFocus.787314EB",
            "keys": "ctrl+shift+tab"
        }
    ],
```
