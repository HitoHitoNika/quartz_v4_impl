```dataview
table topic as Thema
from "Berufsschule"
where contains(file.tags, "LF3")
sort file.name ASC
```

