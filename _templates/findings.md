---
created: 2025-12-29T10:20
updated: 2025-12-29T12:06
---
<%*
const topic = await tp.system.prompt("Topic (bv. findability)");
const subtopic = await tp.system.prompt("Subtopic (optioneel)", "");
const scope = await tp.system.prompt("Scope (bv. 2023-10-10 → 2024-01-08)");
const source = await tp.system.prompt("Source (bv. click data)");
const slug = (s) => (s ?? "")
  .toLowerCase()
  .trim()
  .replace(/\s+/g, "-")
  .replace(/[^a-z0-9/_-]/g, "");

await app.fileManager.processFrontMatter(tp.config.target_file, (fm) => {
  // ... jouw andere velden

  const tags = [];
  if (topic) tags.push(`${slug(topic)}`);
  if (subtopic) tags.push(`${slug(subtopic)}`);

  // combineer met bestaande tags als die er al zijn
  fm.type = "[[finding]]";
  fm.topic = `[[${topic}]]`;
  if (subtopic) fm.subtopic = `[[${subtopic}]]`;
  fm.scope = scope;
  fm.source = `[[${source}]]`;
  fm.date = tp.date.now("YYYY-MM-DD");
  fm.tags = Array.from(new Set([...(fm.tags ?? []), ...tags]));
});
%>
## Finding
**<%* tR += await tp.system.prompt("Kernzin van de finding") %>**

## Context
<%* tR += await tp.system.prompt("Korte context / uitleg", "") %>

## Implications
- <%* tR += await tp.system.prompt("Implicatie (optioneel)", "") %>

## Evidence
<!-- voeg screenshots/links toe -->
