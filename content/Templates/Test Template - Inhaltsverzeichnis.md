```dataview
table topic as Thema
from "Berufsschule"
where contains(file.tags, "LF3")
sort file.name ASC
```

<%*
const dv = app.plugins.plugins["dataview"].api;
const filename = "Inhaltsverzeichnis Lernfeld 3";
const query = `
table topic as Thema
from "Berufsschule"
where contains(file.tags, "LF3")
sort file.name ASC`;
const tFile = tp.file.find_tfile(filename);
const queryOutput = await dv.queryMarkdown(query); 
// write query output to file
await app.vault.modify(tFile, queryOutput.value); %>
%>
