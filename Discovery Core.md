---
created: 2026-05-05T07:21
updated: 2026-05-14T08:04
---
Backlog:
- [x] improve prompt laplace to prevent usage of other agents ✅ 2026-05-10
- [ ] connect linnaeus to product data
- [x] add elastic mcp for argus and adjust prompt ✅ 2026-05-10
- [ ] adjust prompts and context to emphasize certain topics less
- [ ] add tracking issues page for Turing
- [ ] add commands to the interface
- [x] layout (extra regel afstand, link kleur) ✅ 2026-05-10
- [ ] add click_data_master as 'alias' and mention it in descartes prompt
- [ ] investigate if laplace should use dbt skills to 'get model details' and such. isn't this up to descartes to do? 
- [ ] create fork with broader context to support full buying journey
- [ ] add a seasonality analysis to context/wiki
- [ ] add more UX context and content
- [ ] add product content + context
- [ ] hoe kunnen we obsidian web clipper gebruiken icm de custom UI? 
- [ ] add simpsons paradox to ... laplace?

## FAQ
### why do we need an orchestrator for single domain questions? 
Laplace does a few things that add value and benefits the overall performance and efficiency of getting to the answer: 
- it can determine if the question truly is one dimensional/one single domain
- it can use a more expensive model where its needed and adds value; thinking through to determine what data to retrieve is more difficult than actually retrieving the data. proper instructions to descartes for analysis for instance benefit the efficiency and quality of the output
- it can combine and interpret multiple signals to come to follow up questions and tasks and the best answer
- it acts as a 'consultant' in translating detailed technical output into business language; ie. 'the trend is a steady increase' instead of numbers per week in a table. 
it mainly comes down to; translating a business question into more precise instructions and translating the output back to the user in a way its best understood

