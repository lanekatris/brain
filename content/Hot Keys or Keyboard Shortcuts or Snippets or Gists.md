
| App      | Key                         | Action                              |
| -------- | --------------------------- | ----------------------------------- |
| Webstorm | `alt+J`                     | Select next occurrence              |
| Vim      | `gv`                        | Re-select last selected visual area |
| Vim      | `:s` `/foo/bar/g`           | Find / Replace                      |
| Webstorm | `ctrl+F12`                  | View All Methods of Current File    |
| KDE      | `alt-f2`  `kwin --replace`  | Reset KDE UI                        |
| Obsidian | `ctrl+win+<-` `ctrl+win+->` | Navigate panes                      |
| Datagrip | SHIFT + Mouse Wheel         | Horizontally Scroll                 |

[Extract first 10 lines of file](https://stackoverflow.com/questions/28908638/extract-only-the-first-10-lines-of-a-csv-file-in-powershell)
````powershell
Get-Content "C:\start.csv" | select -First 10 | Out-File "C:\stop.csv"
````

### QSV
```bash
./qsv apply datefmt "Log DateTime" --formatstr '%Y-%m-%d' file.csv | ./qsv select 1
```