To delete line feeds that are non-followed by a horizontal rule or a table with the Regex Find/Replace Obsidian community's plugin: 
```regex
^\s*\n(?!---)(?!\|[\s\w]+)
```
