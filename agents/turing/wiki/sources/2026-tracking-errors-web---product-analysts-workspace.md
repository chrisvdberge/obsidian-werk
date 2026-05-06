---
Type: source
Tags:
  - source
  - turing
Agent: turing
Source: https://kramphub.atlassian.net/wiki/spaces/XP/pages/6960414854/Tracking+errors+web
Analysed: 2026-05-05
Data-period: 2026-05-05
Model:
Freshness: Stable
created: 2026-05-05T13:51
updated: 2026-05-05T13:51
---

# Tracking errors web - Product Analysts workspace

**Source:** https://kramphub.atlassian.net/wiki/spaces/XP/pages/6960414854/Tracking+errors+web
**Clipped:** 2026-05-05

## Summary



## Content

## Tracking errors web

This page is logging the excising and fixed bugs in the tracking on the website. Ordered from newest bugs to oldest bugs.  

Impact is assessed based on the impact the issue had on metrics and how they are used. This means the focus is on processed data in BigQuery and how metrics are used in experiments and dashboards. Usage of GA4 interface itself is not taken into account. A low impact issue could still be very high when considering using GA4.  
Example: double npc issue: This is accounted for in the processing of the data.

- double events are excluded when they happen on the same timestamp
- most metrics use distinct counts of events per product per customer per visit (or day)

This means the *product interest* metric and counts for net price checks on certain products is not affected. However, if you would go into GA4 to look up this information you’d see inflated counts.

<table><colgroup><col> <col> <col> <col> <col> <col> <col> <col></colgroup><tbody><tr><th rowspan="1" colspan="1"><div><p><strong>Event</strong></p><figure></figure></div></th><th rowspan="1" colspan="1"><div><p><strong>Context</strong></p><figure></figure></div></th><th rowspan="1" colspan="1"><div><p><strong>KPI Impact</strong></p><figure></figure></div></th><th rowspan="1" colspan="1"><div><p><strong>Issue</strong></p><figure></figure></div></th><th rowspan="1" colspan="1"><div><p><strong>Start</strong></p><figure></figure></div></th><th rowspan="1" colspan="1"><div><p><strong>Fixed</strong></p><figure></figure></div></th><th rowspan="1" colspan="1"><div><p><strong>Duration</strong></p><figure></figure></div></th><th rowspan="1" colspan="1"><div><p><strong>Ticket</strong></p><figure></figure></div></th></tr></tbody></table>

<table><colgroup><col> <col> <col> <col> <col> <col> <col> <col></colgroup><tbody><tr><th rowspan="1" colspan="1"><div><p><strong>Event</strong></p><figure></figure></div></th><th rowspan="1" colspan="1"><div><p><strong>Context</strong></p><figure></figure></div></th><th rowspan="1" colspan="1"><div><p><strong>KPI Impact</strong></p><figure></figure></div></th><th rowspan="1" colspan="1"><div><p><strong>Issue</strong></p><figure></figure></div></th><th rowspan="1" colspan="1"><div><p><strong>Start</strong></p><figure></figure></div></th><th rowspan="1" colspan="1"><div><p><strong>Fixed</strong></p><figure></figure></div></th><th rowspan="1" colspan="1"><div><p><strong>Duration</strong></p><figure></figure></div></th><th rowspan="1" colspan="1"><div><p><strong>Ticket</strong></p><figure></figure></div></th></tr><tr><td rowspan="1" colspan="1"><p>page_view</p></td><td rowspan="1" colspan="1"><p>partsfinder</p></td><td rowspan="1" colspan="1"><p>Low</p></td><td rowspan="1" colspan="1"><p>double pageview on partsfinder page, one of them is missing <strong>shopping_cart_id</strong></p></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"></td></tr><tr><td rowspan="1" colspan="1"><p>page_view</p><p>view_item</p></td><td rowspan="1" colspan="1"><p>search</p></td><td rowspan="1" colspan="1"><p>Very high</p></td><td rowspan="1" colspan="1"><p>On PDP, <strong>missing search_id</strong> and <strong>search_term</strong>.</p><p>When searching on a PDP, the search_id and search_term are missing on the page_view and view_item event.</p></td><td rowspan="1" colspan="1"><p>Aug 20, 2025</p></td><td rowspan="1" colspan="1"><p>Aug 22, 2025</p></td><td rowspan="1" colspan="1"><p>3 days</p></td><td rowspan="1" colspan="1"><p><a href="https://kramphub.atlassian.net/browse/FINDTY-1090">https://kramphub.atlassian.net/browse/FINDTY-1090</a></p></td></tr><tr><td rowspan="1" colspan="1"><p>npc</p></td><td rowspan="1" colspan="1"><p>product metrics</p></td><td rowspan="1" colspan="1"><p>Low</p></td><td rowspan="1" colspan="1"><p>double NPC event on bulk discount price check</p></td><td rowspan="1" colspan="1"><p>Jun 25, 2025 (bug reported)</p></td><td rowspan="1" colspan="1"><p>Jul 4, 2025</p></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"></td></tr><tr><td rowspan="1" colspan="1"><p>page_view</p></td><td rowspan="1" colspan="1"><p>partsfinder, make model</p></td><td rowspan="1" colspan="1"><p>High</p></td><td rowspan="1" colspan="1"><p>On partsfinder page, we are missing <strong>content_id</strong> and <strong>content_group</strong></p></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"><p><a href="https://kramphub.atlassian.net/browse/FINDTY-1061">https://kramphub.atlassian.net/browse/FINDTY-1061</a></p></td></tr><tr><td rowspan="1" colspan="1"><p>page_view</p><p>view_item</p></td><td rowspan="1" colspan="1"><p>product, recommenders</p></td><td rowspan="1" colspan="1"><p><mark>Very high</mark></p></td><td rowspan="1" colspan="1"><p>On PDP, after a select_item in a product_list (recommender), the page_view and view_item event is <strong>not triggered</strong>. Also, when using search suggestion after the product_list click.</p><p>After using product_list on PDP → search on that PDP for a search term → search results page → click on a product → the concent_group and content_id of the PDP is empty in page_view and view_item.</p><img src="blob:https://kramphub.atlassian.net/70c0f420-56a9-427f-b5b7-0bbf328d0d0f#media-blob-url=true&id=fa533379-da81-4917-b7d8-1da432e4219d&collection=contentId-6960414854&contextId=6960414854&width=424&height=275&alt=image-20250815-114438.png&clientId=7c912ce3-649f-477a-89f5-fb5d365192be"></td><td rowspan="1" colspan="1"><p>Aug 12, 2025</p></td><td rowspan="1" colspan="1"><p>Aug 19, 2025</p></td><td rowspan="1" colspan="1"><p>8 days</p></td><td rowspan="1" colspan="1"><p><a href="https://kramphub.atlassian.net/browse/FINDTY-1075">https://kramphub.atlassian.net/browse/FINDTY-1075</a></p></td></tr><tr><td rowspan="1" colspan="1"><p>view_cart</p></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"><p>Low</p></td><td rowspan="1" colspan="1"><p>The view_cart event is <strong>triggering twice</strong> in the following scenario: from shopping cart → PDP → add product → shopping cart. It’s not on page load, but after visiting PDP/adding products to cart.</p><img src="blob:https://kramphub.atlassian.net/8fa346e1-c50c-4f9a-8b0e-fed0974a0b01#media-blob-url=true&id=cc3aac0d-83e6-4904-a683-9c92c067308c&collection=contentId-6960414854&contextId=6960414854&width=678&height=299&alt=image-20250805-135616.png&clientId=7c912ce3-649f-477a-89f5-fb5d365192be"></td><td rowspan="1" colspan="1"><p>Jul 30, 2025</p></td><td rowspan="1" colspan="1"><p><em>not fixed</em></p></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"><p><a href="https://kramphub.atlassian.net/browse/COV-1153">https://kramphub.atlassian.net/browse/COV-1153</a></p></td></tr><tr><td rowspan="1" colspan="1"><p>view_cart</p></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"><p>Low</p></td><td rowspan="1" colspan="1"><p>The view_cart event <strong>isn’t tracking products</strong> anymore.</p><p></p><pre><code>dataLayer.push({ ecommerce: null });

dataLayer.push({

  event: "view_cart",

  content_group: "shopping_cart",

  content_id: "106272586",

  ecommerce: {

    items: Array(0)

;</code></pre><p></p><img src="blob:https://kramphub.atlassian.net/c2b211ad-8632-480f-8b47-48408f659606#media-blob-url=true&id=9fa2c367-5fdc-4164-b72b-75f41a0a6716&collection=contentId-6960414854&contextId=6960414854&width=690&height=428&alt=image-20250731-093423.png&clientId=7c912ce3-649f-477a-89f5-fb5d365192be"></td><td rowspan="1" colspan="1"><p>Jul 30, 2025</p></td><td rowspan="1" colspan="1"><p>Aug 6, 2025</p></td><td rowspan="1" colspan="1"><p>6 days</p></td><td rowspan="1" colspan="1"><p><a href="https://kramphub.atlassian.net/browse/COV-1142">https://kramphub.atlassian.net/browse/COV-1142</a></p></td></tr><tr><td rowspan="1" colspan="1"><p>add_shipping_</p><p>info</p></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"><p>Low</p></td><td rowspan="1" colspan="1"><p>Since 4th of September 2024, the add_shipping_info event was incorrectly being triggered when a customer entered the checkout. This is fixed since 24th of July 2025.</p><img src="blob:https://kramphub.atlassian.net/63491ca7-92ad-4b58-8f2e-8b4f4119b890#media-blob-url=true&id=0283514e-3910-4445-b02c-f439509d212d&collection=contentId-6960414854&contextId=6960414854&width=1075&height=351&alt=image-20250821-132110.png&clientId=7c912ce3-649f-477a-89f5-fb5d365192be"></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"><p>Jul 24, 2025</p></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"><p><a href="https://kramphub.atlassian.net/browse/COV-795">https://kramphub.atlassian.net/browse/COV-795</a></p></td></tr><tr><td rowspan="1" colspan="1"><p>page_view</p></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"><p>High</p></td><td rowspan="1" colspan="1"><p>Due to an overall front-end update, the page_view and view_cart event <strong>triggered too much</strong>. Issue occurred on the following pages:</p><p>Checkout - Wishlist - Shopping cart - Product - Promotion</p><img src="blob:https://kramphub.atlassian.net/745ff48e-0aaf-4419-98f4-4185c0cbb0ae#media-blob-url=true&id=a60c3f52-8966-45be-8929-9462c5769dd5&collection=contentId-6960414854&contextId=6960414854&width=854&height=380&alt=image-20250507-092315.png&clientId=7c912ce3-649f-477a-89f5-fb5d365192be"></td><td rowspan="1" colspan="1"><p>May 6, 2025</p></td><td rowspan="1" colspan="1"><p>May 8, 2025</p></td><td rowspan="1" colspan="1"><p>3 days</p></td><td rowspan="1" colspan="1"><p><a href="https://kramphub.atlassian.net/browse/FPT-1068">https://kramphub.atlassian.net/browse/FPT-1068</a></p></td></tr><tr><td rowspan="1" colspan="1"><p>double events on search</p></td><td rowspan="1" colspan="1"><p>search</p></td><td rowspan="1" colspan="1"><p>Low</p></td><td rowspan="1" colspan="1"><p>We trigger too many events when people perform a new search from the search result page (so not via other pages).<br><br>a previously fixed error that came back.</p></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"><p><a href="https://kramphub.atlassian.net/browse/FINDTY-666">https://kramphub.atlassian.net/browse/FINDTY-666</a></p></td></tr><tr><td rowspan="1" colspan="1"><p>npc in wishlist</p></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"><p>Low</p></td><td rowspan="1" colspan="1"><p>No NPC event being triggered in the wishlist</p><img src="blob:https://kramphub.atlassian.net/910e1e52-ba95-444e-9923-1fe9455b30f3#media-blob-url=true&id=8fea7045-1de2-46b3-b4be-84535ab08058&collection=contentId-6960414854&contextId=6960414854&width=1321&height=494&alt=image-20250806-092843.png&clientId=7c912ce3-649f-477a-89f5-fb5d365192be"></td><td rowspan="1" colspan="1"><p>Mar 28, 2025</p></td><td rowspan="1" colspan="1"><p>Jul 1, 2025</p></td><td rowspan="1" colspan="1"><p>34 days</p></td><td rowspan="1" colspan="1"><p>x</p></td></tr><tr><td rowspan="1" colspan="1"><p>atp</p></td><td rowspan="1" colspan="1"><p>product</p></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"><p>ATP event <strong>triggers twice</strong> after click. Issue occurs on all pages.</p><img src="blob:https://kramphub.atlassian.net/9aa1c079-ce31-4875-8b8a-3bdfa5776be9#media-blob-url=true&id=640f0511-c55d-432e-954d-bdb5cc102b1e&collection=contentId-6960414854&contextId=6960414854&width=1084&height=354&alt=image-20250527-120721.png&clientId=7c912ce3-649f-477a-89f5-fb5d365192be"></td><td rowspan="1" colspan="1"><p>May 14, 2025</p></td><td rowspan="1" colspan="1"><p>Sep 11, 2025</p></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"><p><a href="https://kramphub.atlassian.net/browse/DTB-1197">https://kramphub.atlassian.net/browse/DTB-1197</a></p></td></tr><tr><td rowspan="1" colspan="1"><p>view_item</p></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"><p>view_item event triggered twice when navigating from search, categories and recommendations</p></td><td rowspan="1" colspan="1"><p>May 28, 2025</p></td><td rowspan="1" colspan="1"><p>Jun 19, 2025</p></td><td rowspan="1" colspan="1"><p>22 days</p></td><td rowspan="1" colspan="1"><p><a href="https://kramphub.atlassian.net/browse/DTB-1213">https://kramphub.atlassian.net/browse/DTB-1213</a></p></td></tr><tr><td rowspan="1" colspan="1"><p>add_to_cart</p></td><td rowspan="1" colspan="1"><p>search</p></td><td rowspan="1" colspan="1"><p>Medium</p></td><td rowspan="1" colspan="1"><p>search dimensions missing on an add to cart in the blue box<br>search_id is there, so impact medium</p></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"><p><a href="https://kramphub.atlassian.net/browse/FINDTY-825">https://kramphub.atlassian.net/browse/FINDTY-825</a></p></td></tr><tr><td rowspan="1" colspan="1"><p>page_view</p></td><td rowspan="1" colspan="1"><p>make model</p></td><td rowspan="1" colspan="1"><p>Low</p></td><td rowspan="1" colspan="1"><p>missing breadcrumb on composedproduct pages</p></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"><p><a href="https://kramphub.atlassian.net/browse/FINDTY-864">https://kramphub.atlassian.net/browse/FINDTY-864</a></p></td></tr><tr><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"><p>search</p></td><td rowspan="1" colspan="1"><p>Medium</p></td><td rowspan="1" colspan="1"><p>missing search_id and other search dimensions on specific scenario:<br></p><ul><li><p>search for battery</p></li><li><p>click item</p></li><li><p>search for 100100 and click product suggestion</p></li><li><p>use back button to go back to the pdp of the battery</p></li></ul><p>now search is empty, no search id or search term are send on any subsequent events</p></td><td rowspan="1" colspan="1"><p>Mar 10, 2025</p></td><td rowspan="1" colspan="1"><p><em>fixed automagically</em></p></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"><p><a href="https://kramphub.atlassian.net/browse/FINDTY-586">https://kramphub.atlassian.net/browse/FINDTY-586</a></p></td></tr><tr><td rowspan="1" colspan="1"><p>page_view</p></td><td rowspan="1" colspan="1"><p>category</p></td><td rowspan="1" colspan="1"><p>Medium</p></td><td rowspan="1" colspan="1"><p>missing content_group and content_id on level 1 and level 2 category pages</p></td><td rowspan="1" colspan="1"><p>Sep 8, 2024</p></td><td rowspan="1" colspan="1"><p>Mar 3, 2025</p></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"><p><a href="https://kramphub.atlassian.net/browse/FINDTY-493">https://kramphub.atlassian.net/browse/FINDTY-493</a></p></td></tr><tr><td rowspan="1" colspan="1"><p>all</p></td><td rowspan="1" colspan="1"><p>search</p></td><td rowspan="1" colspan="1"><p>Very high</p></td><td rowspan="1" colspan="1"><p>mixed search_id and search_term when using back button to go from 2nd search to results of 1st search<br></p><img src="blob:https://kramphub.atlassian.net/85eafd20-2b41-42d0-9574-2289ec86ffe1#media-blob-url=true&id=954ed977-1421-4d1b-ab98-0ca81260b06a&collection=contentId-6960414854&contextId=6960414854&width=1088&height=646&alt=image-20260403-101603.png&clientId=7c912ce3-649f-477a-89f5-fb5d365192be"><p><span></span></p><pre><code>WITH visit_stats AS (

    SELECT

        webshop_visit_id,

        webshop_event_date,

        COALESCE(webshop_user, client) AS identifier,

        MAX(webshop_user) AS webshop_user,

        MAX(customer_cd) AS customer_cd,

        COUNT(*) AS total_events,

        COUNT(DISTINCT CASE WHEN npc > 0 THEN product_cd END) AS npcs,

        COUNT(DISTINCT CASE WHEN atp > 0 THEN product_cd END) AS atps,

        SUM(CASE WHEN ws_event_name = 'page_view' AND page_path LIKE '%/p/%' THEN 1 ELSE 0 END) AS pdps,

        SUM(CASE WHEN ws_event_name = 'view_search_results' THEN 1 ELSE 0 END) AS searches,

        COUNT(

            CASE

                WHEN search_method LIKE "%'%"

                  OR search_type LIKE "% OR %"

                  OR search_type LIKE "%'%"

                  OR (page_path LIKE "% OR %" AND content_group <> "search")

                THEN 1

            END

        ) AS hard_pollution_events

    FROM `kg-data-e-commerce-prd.presentation_common.pres__obt__click_data_master`

    WHERE webshop_event_date >= DATE '2026-01-01'

    GROUP BY 1, 2, 3

),

daily_stats AS (

    SELECT

        identifier,

        webshop_event_date,

        COUNT(DISTINCT webshop_visit_id) AS daily_visits

    FROM visit_stats

    GROUP BY 1, 2

),

outlier AS (

    SELECT

        v.webshop_visit_id

    FROM visit_stats v

    LEFT JOIN daily_stats d

        ON v.identifier = d.identifier

       AND v.webshop_event_date = d.webshop_event_date

    WHERE v.hard_pollution_events > 0

       OR v.total_events > 1000

       OR v.npcs > 1000

       OR v.atps > 1000

       OR v.pdps > 1000

       OR v.searches > 500

       OR (d.daily_visits > 50 AND v.total_events <= 10)

),

searches_base AS (

    SELECT

        s.search_event_date,

        s.searches,

        s.success,

        s.webshop_visit_id

    FROM `kg-data-e-commerce-prd.presentation_common.pres__obt__searches_mapped_master` s

    WHERE s.search_event_date >= DATE '2024-01-01'

),

search2024 AS (

    SELECT

        EXTRACT(ISOWEEK FROM search_event_date) AS week_nr,

        SAFE_DIVIDE(SUM(success), SUM(searches)) AS ssr_2024

    FROM searches_base

    WHERE search_event_date BETWEEN DATE '2024-01-01' AND DATE '2024-12-31'

    GROUP BY 1

),

search2025 AS (

    SELECT

        EXTRACT(ISOWEEK FROM search_event_date) AS week_nr,

        SAFE_DIVIDE(SUM(success), SUM(searches)) AS ssr_2025

    FROM searches_base

    WHERE search_event_date BETWEEN DATE '2025-01-01' AND DATE '2025-12-31'

    GROUP BY 1

),

search2026_incl AS (

    SELECT

        EXTRACT(ISOWEEK FROM search_event_date) AS week_nr,

        SAFE_DIVIDE(SUM(success), SUM(searches)) AS ssr_2026_no_filter

    FROM searches_base

    WHERE search_event_date BETWEEN DATE '2026-01-01' AND DATE '2026-12-31'

    GROUP BY 1

),

search2026_excl AS (

    SELECT

        EXTRACT(ISOWEEK FROM sb.search_event_date) AS week_nr,

        SAFE_DIVIDE(SUM(sb.success), SUM(sb.searches)) AS ssr_2026_filtered

    FROM searches_base sb

    LEFT JOIN outlier o

        ON sb.webshop_visit_id = o.webshop_visit_id

    WHERE sb.search_event_date BETWEEN DATE '2026-01-01' AND DATE '2026-12-31'

      AND o.webshop_visit_id IS NULL

    GROUP BY 1

)

SELECT

    COALESCE(a.week_nr, b.week_nr, c.week_nr, d.week_nr) AS week_nr,

    a.ssr_2024,

    b.ssr_2025,

    c.ssr_2026_no_filter,

    d.ssr_2026_filtered

FROM search2024 a

FULL OUTER JOIN search2025 b USING (week_nr)

FULL OUTER JOIN search2026_incl c USING (week_nr)

FULL OUTER JOIN search2026_excl d USING (week_nr)

ORDER BY week_nr</code></pre><p></p></td><td rowspan="1" colspan="1"><p>Nov 17, 2024<br>Estimate</p></td><td rowspan="1" colspan="1"><p>Feb 10, 2025<br>Estimate</p></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"><p><a href="https://kramphub.atlassian.net/browse/FINDTY-523">https://kramphub.atlassian.net/browse/FINDTY-523</a></p></td></tr><tr><td rowspan="1" colspan="1"><p>all</p></td><td rowspan="1" colspan="1"><p>search</p></td><td rowspan="1" colspan="1"><p>Very high</p></td><td rowspan="1" colspan="1"><p>mixed search_id and search_term when using back button from clicked product_suggestion to go back to previous search results</p></td><td rowspan="1" colspan="1"><p>Nov 17, 2024<br>Estimate</p></td><td rowspan="1" colspan="1"><p>Feb 17, 2025<br>Estimate</p></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"><p><a href="https://kramphub.atlassian.net/browse/FINDTY-542">https://kramphub.atlassian.net/browse/FINDTY-542</a></p></td></tr><tr><td rowspan="1" colspan="1"><p>all</p></td><td rowspan="1" colspan="1"><p>search</p></td><td rowspan="1" colspan="1"><p>High</p></td><td rowspan="1" colspan="1"><p>no new search_id generated when user goes to search results without search action.<br>ie; user can change the url and adjust the query there.<br>all searches will have the same search_id now</p></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"><p><a href="https://kramphub.atlassian.net/browse/FINDTY-493">https://kramphub.atlassian.net/browse/FINDTY-493</a></p></td></tr><tr><td rowspan="1" colspan="1"><p>view_item_list</p></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"><p>High</p></td><td rowspan="1" colspan="1"><p>On the PDP, instead of view_item_list a view_item event was triggered for products in the product lists.</p><img src="blob:https://kramphub.atlassian.net/fb59de4f-4eae-4601-a44e-f4bfe9f2ec17#media-blob-url=true&id=5a00b62d-11da-41cc-8a49-b591b69a5c80&collection=contentId-6960414854&contextId=6960414854&width=1020&height=477&alt=image-20250821-134517.png&clientId=7c912ce3-649f-477a-89f5-fb5d365192be"></td><td rowspan="1" colspan="1"><p>Oct 1, 2024</p></td><td rowspan="1" colspan="1"><p>Oct 21, 2024</p></td><td rowspan="1" colspan="1"><p>21 days</p></td><td rowspan="1" colspan="1"></td></tr><tr><td rowspan="1" colspan="1"><p>add_to_cart</p></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"></td><td rowspan="1" colspan="1"><p>Incorrect content_id in ATC event on PDP.</p></td><td rowspan="1" colspan="1"><p>Jan 1, 2024</p></td><td rowspan="1" colspan="1"><p>Sep 5, 2024</p></td><td rowspan="1" colspan="1"><p>247 days</p></td><td rowspan="1" colspan="1"></td></tr></tbody></table>

Unfold “tracking milestones and bugs” for timeline overview of bugs.

<iframe src="https://kramphub.atlassian.net/rest/greenhopper/1.0/roadmap/fragment/confluenceMacro/CDM?boardId=935&amp;fragmentHost=https%3A%2F%2Fkramphub.atlassian.net&amp;themeState=dark%3Adark+light%3Alight+spacing%3Aspacing+typography%3Atypography+colorMode%3Alight" allowfullscreen="" allow="autoplay; encrypted-media; clipboard-write" title="Click data management | Timeline"></iframe>

Related content

## See also

- [turing wiki index](../INDEX.md)
- [Shared wiki index](../../../wiki/index.md)