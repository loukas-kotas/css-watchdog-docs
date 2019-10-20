# CLI

## 1. View help
```watchdog --help```

## 2. Get screenshot of whole page
```watchdog screenshot-page <source> <path-to-save>```

| Parameter | Description |
| --------- | ----------- |
| source    | url of page to get the screenshot |
| path-to-save | where to save the screenshot   |

**Example**

```watchdog screenshot-page https://loukaskotas.com assets```

## 3. Get screenshot of part of the page
```watchdog screenshot-part-page <source> <path-to-save> <x0> <y0> <x1> <y1>```

| Parameter    | Description |
| ------------ | ----------- |
| source       | url of page to get the screenshot |
| path-to-save | where to save the screenshot      |
| x0           | starting point x-axis             |
| y0           | starting point y-axis             |
| x1           | ending point x-axis               |
| y1           | ending point y-axis               |

**Example**

```watchdog screenshot-part-page https://loukaskotas.com assets 0 0 100 100```
