---
created: 2026-05-06T15:39
updated: 2026-05-07T13:11
---
- users need to add secret files with dbt token and elastic API key via terminal. that's not practical for exposing the tool to many business users and not desired since I'd have to share the token with too many people
- it has build and plan agents. people can ask to make changes. dont want that
- need/can choose model. 
	- defauilt agent works, but it has sonnet instead of opus selected
- output not filtered. tool calls, subagent calls etc. all visible to the user. 
	- compared to our custom UI
	- ![[Scherm­afbeelding 2026-05-06 om 15.45.14.png]]![[Scherm­afbeelding 2026-05-06 om 15.45.42.png]]
- output is not filtered, but at the same time the tool calls and executions are not fully visible. 
	- we have this in admin view. good to check sql statements executed, api calls done etc. 
- no control over or possibility to add things to context and memory
- no feedback option on the chat. (used to improve agents)
- 