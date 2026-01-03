---
created: 2025-12-03T20:37
updated: 2025-12-03T20:39
---


nu kom ik bijv. op ticItemGroup-112707980 uit, maar als ik die op de site probeer te openen krijg ik een error. 

als ik items probeer te zoeken/vinden die buyable zouden zijn, dan krijg ik continu het scenario in Elastic dat er wel 1 resultaat terugkomt, maar dat die achteraf nog wordt gefilterd (door... envy?)

bijv. `UNTH00666` in NL

als ik de Elastic index check, dan staat daar dat die `base_NL` als assortment heeft, `attBuyableInCountry` heeft als waarde belgie en nederland. 

market is `NL_Internal` though, 

toch als ik de GBQ tabellen hanteer dan heeft die ook wel buyable = Yes. 

weet jij wat hier precies gebeurd? 

Het zal aan mijn demo account liggen die die markt wel heeft. Maar dan filtert Envy anders dan dat wij doen. 

voor de duidelijkheid; ik zie dit met een demo account, maar met mijn persoonlijke account krijg ik 'netjes' 0 results. 

Blijft alleen nog wel de vraag of jij weet hoe ik dit zou kunnen mee nemen met het inschatten van item aantallen in groups? 

want `kramp-sharedmasterdata-prd.kramp_sharedmasterdata_customquery.TBL__CMQ__dcm__PLM__latest` heeft niet expliciet de markt erin, en zegt gewoon dat het buyable is


een ander voorbeeld heeft echter wel echt `NL` als market

C2K04265A

assortment_id is `base_NL` EN `CSI_AS_C2K04265A`

dus deze lijkt customer specific maar OOK baseNL ? 

Deze krijg ik _wel_ terug ook op mijn persoonlijke account en die wordt vervolgens niet weergegeven. 

interestingly enough is `attTemproarilyNotBuyable` zowel 'No' als 'Yes' in onze index. dus wellicht zit daar wat in ?  oh wait.. ik zie dit; 

     "attTemporarilyNotBuyableInCountry": "Ireland",

      "attBuyableInCountry": "Netherlands",

dus even een surprise waarom ik hem in NL dan toch niet zie

```sql
with a as (
 select distinct
 product_number,
itemgroup_id,
assortment_type,
 PLMstatuscode,
 buyable,
 country

 from `kramp-sharedmasterdata-prd.kramp_sharedmasterdata_customquery.CMQ__product_wholesale` p
 left join `kramp-sharedmasterdata-prd.kramp_sharedmasterdata_customquery.TBL__CMQ__dcm__PLM__latest` as plm on p.product_number = plm.itemnumber
 where 1=1
--  and csbu in ('Denmark')
)

select 
itemgroup_id, 
assortment_type,
-- country,
count(distinct case when plmstatuscode in ('700') then product_number else NULL end) as plm_nonbuyable_visible,
count(distinct case when plmstatuscode in ('400','500','600') then product_number else NULL end) as plm_buyable,
count(distinct case when buyable = 'Yes' then product_number else NULL end) as plm_buyable_flag,
from a
-- where country_code is not null
-- and country_code <> 'ANY'
group by all
-- having plm_buyable = 0
-- and plm_nonbuyable_visible =1

order by plm_nonbuyable_visible desc
```
![[Scherm­afbeelding 2025-12-03 om 20.39.10.png]]