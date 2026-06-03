---
created: 2026-05-05T07:21
updated: 2026-06-02T17:02
---
Backlog:
- [x] improve prompt laplace to prevent usage of other agents ✅ 2026-05-10
- [ ] connect linnaeus to product data
- [x] add elastic mcp for argus and adjust prompt ✅ 2026-05-10
- [ ] adjust prompts and context to emphasize certain topics less
	- [ ] create fact triplets
- [ ] add tracking issues page for Turing
- [ ] add commands to the interface
- [x] layout (extra regel afstand, link kleur) ✅ 2026-05-10
- [ ] add click_data_master as 'alias' and mention it in descartes prompt
	- [ ] create common glossary
- [ ] investigate if laplace should use dbt skills to 'get model details' and such. isn't this up to descartes to do? 
- [x] create fork with broader context to support full buying journey ✅ 2026-05-27
- [x] add a seasonality analysis to context/wiki ✅ 2026-05-27
	- [x] adjust the lag days. check about up and down effects of lag days ✅ 2026-05-28
- [ ] add more UX context and content
- [ ] add product content + context
- [ ] hoe kunnen we obsidian web clipper gebruiken icm de custom UI? 
- [ ] add simpsons paradox to ... laplace?
	- [ ] datascientist
	-

## FAQ
### why do we need an orchestrator for single domain questions? 
Laplace does a few things that add value and benefits the overall performance and efficiency of getting to the answer: 
- it can determine if the question truly is one dimensional/one single domain
- it can use a more expensive model where its needed and adds value; thinking through to determine what data to retrieve is more difficult than actually retrieving the data. proper instructions to descartes for analysis for instance benefit the efficiency and quality of the output
- it can combine and interpret multiple signals to come to follow up questions and tasks and the best answer
- it acts as a 'consultant' in translating detailed technical output into business language; ie. 'the trend is a steady increase' instead of numbers per week in a table. 
it mainly comes down to; translating a business question into more precise instructions and translating the output back to the user in a way its best understood

# installation
1. open folder ~/gcs/projects
2. launch opencode
3. rechts onderin 'open preview'
4. kies project
5. ask agent to clone "~/gcs/projects/[repo]"
6. ga naar de workstation, daar is een popup met git authentication
7. cloned
8. dbt toegang

```
mkdir -p .opencode/.secrets
echo "YOUR_DBT_TOKEN" > .opencode/.secrets/dbt-token
echo "YOUR_DBT_USER_ID" > .opencode/.secrets/dbt-user-id
echo "ES_API_TOKEN" > .opencode/.secrets/es-api-token
```


# awesome examples
Laplace gets input from data-scientist that a table is empty. wants to verify with Descartes;
```
I need an independent verification of a claim about the experimentation data warehouse. Another analyst reported that `pres__dim__experimentation_treatment_assignments` is **completely empty** (0 rows across all experiments) due to an inverted `NOT IN` filter in the model SQL. This would block ALL experiment analyses, so I want a second pair of eyes before treating it as a confirmed data incident.
```

comparison to looker
- admin available
- supressing output not possible currently

meeting looker
openai openai openai
huge instruction prompt

# test questions
- search results question: 
```
If I search for 020140, why do I see product 100100 in the search results?
```
- responses
	- 2026-06-02, laplace on opus 4.8
	- ```
	  I'll diagnose this search-relevance question. First, let me classify the query: `020140` is an item/product ID (numeric), so this is language-independent — I can delegate to @argus immediately without asking for a market.

[

](https://24672-ws-christian-van-den-berge.cluster-hsrqhqiztrawsr66n3eyoorfya.cloudworkstations.dev/L2hvbWUvdXNlci9nY3MvcHJvamVjdHMvZmluZGFiaWxpdHktb3BlbmNvZGUtYWdlbnRpYy1wcm9kdWN0LWRpc2NvdmVyeQ/session/ses_17727d8daffec450yI8cH3Z8Wv)

**Searching `020140` returns product 100100 because product 100100 lists `020140` as a number it replaces — `020140` is an old/superseded article number that 100100 took over — and also as a competitor cross-reference. So searching the old number correctly surfaces its Kramp replacement. This is intended behavior, not a search bug.**

One thing worth a closer look (a data-quality note, not a search problem): product 100100 carries an unusually long cross-reference list that includes obvious test/placeholder entries (e.g. `TestStopIt`, `ws 100100`). The `020140` match itself is legitimate, but if you want to verify the broader mapping is clean, that's a question for the data owners of the product's cross-reference enrichment — not a search-engine change.
	  ```
	  