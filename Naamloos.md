---
created: 2026-03-19T11:37
updated: 2026-03-19T11:37
---
# 8 Types of Farming — Agent Context Extract
**Source:** 8_types_of_farming

## Purpose
This file converts the farming-type diagrams into a compact, machine-readable summary for agent use.

## Legend
- `main` = main activity
- `secondary` = lesser activity
- `outsourced_main` = main activity, but likely outsourced to a contractor
- `none` = not indicated for this farming type

## Activity vocabulary
The activity rows used in the source are:

1. tillage_cultivation
2. planting_seeding
3. crop_care
4. fertilizing
5. irrigation
6. harvest
7. barn_management
8. feeding
9. milking
10. slurry_handling
11. storing
12. sorting_packing
13. moving_transport
14. cleaning

## Farming types overview

### TF1 — Field crops
**Definition:** Arable farming of major crops like potatoes, wheat, sugar beets, rice, rapeseed, onions, etc.

**Activity profile**
```yaml
tillage_cultivation: main
planting_seeding: main
crop_care: main
fertilizing: main
irrigation: main
harvest: outsourced_main
barn_management: none
feeding: none
milking: none
slurry_handling: none
storing: main
sorting_packing: main
moving_transport: main
cleaning: main
```

**Interpretation**
- Core workload is field-work and post-harvest handling.
- Livestock-related activities are not part of this type.
- Harvest is important but often contractor-led.

---

### TF2 — Horticulture (indoor/outdoor)
**Definition:** Cultivation of mainly vegetables, flowers, seeds, herbs, mushrooms, and ornamental plants.

**Activity profile**
```yaml
tillage_cultivation: main
planting_seeding: main
crop_care: main
fertilizing: main
irrigation: main
harvest: main
barn_management: none
feeding: none
milking: none
slurry_handling: none
storing: main
sorting_packing: main
moving_transport: main
cleaning: main
```

**Interpretation**
- Strong end-to-end crop workflow from cultivation through handling and cleanup.
- No livestock-management activities.
- More complete downstream handling than broad-acre field crops.

---

### TF3 — Wine
**Definition:** Vineyards, cultivation of grapes.

**Activity profile**
```yaml
tillage_cultivation: main
planting_seeding: secondary
crop_care: main
fertilizing: main
irrigation: main
harvest: main
barn_management: none
feeding: none
milking: none
slurry_handling: none
storing: main
sorting_packing: main
moving_transport: main
cleaning: main
```

**Interpretation**
- Similar to crop-based production, but planting/seeding is less central than for annual crops.
- Strong emphasis on crop care, harvest, and post-harvest handling.
- No livestock activities.

---

### TF4 — Other permanent crops
**Definition:** Products harvested from permanent plants and trees such as olives, fruits, and citrus fruit.

**Activity profile**
```yaml
tillage_cultivation: secondary
planting_seeding: secondary
crop_care: main
fertilizing: main
irrigation: main
harvest: main
barn_management: none
feeding: none
milking: none
slurry_handling: none
storing: main
sorting_packing: main
moving_transport: main
cleaning: main
```

**Interpretation**
- Permanent crops shift effort away from repeated establishment work and toward ongoing maintenance and harvest.
- Crop care, irrigation, and harvest are central.
- No livestock activities.

---

### TF5 — Dairy
**Definition:** Production of milk.

**Activity profile**
```yaml
tillage_cultivation: secondary
planting_seeding: secondary
crop_care: secondary
fertilizing: main
irrigation: secondary
harvest: outsourced_main
barn_management: main
feeding: main
milking: main
slurry_handling: main
storing: main
sorting_packing: none
moving_transport: main
cleaning: main
```

**Interpretation**
- Mixed profile with livestock operations at the center.
- Barn, feeding, milking, slurry, and cleaning are core.
- Some field work exists, mainly to support feed production.
- Harvest matters but is often outsourced.

---

### TF6 — Other grazing livestock
**Definition:** Sheep and cattle for the production of meat and wool.

**Activity profile**
```yaml
tillage_cultivation: secondary
planting_seeding: secondary
crop_care: secondary
fertilizing: main
irrigation: secondary
harvest: outsourced_main
barn_management: main
feeding: main
milking: none
slurry_handling: main
storing: main
sorting_packing: none
moving_transport: main
cleaning: main
```

**Interpretation**
- Similar to dairy in operational pattern, but without milking.
- Core activity is livestock management supported by some land-related work.
- Harvest can still matter, but is commonly contractor-led.

---

### TF7 — Granivores
**Definition:** Pigs and poultry for meat and eggs.

**Activity profile**
```yaml
tillage_cultivation: none
planting_seeding: none
crop_care: none
fertilizing: none
irrigation: none
harvest: none
barn_management: main
feeding: main
milking: none
slurry_handling: main
storing: main
sorting_packing: none
moving_transport: secondary
cleaning: main
```

**Interpretation**
- Predominantly indoor livestock-management model.
- Field activities are not part of the operational core.
- Barn, feeding, slurry, storage, and cleaning are the dominant tasks.

---

### TF8 — Mixed
**Definition:** Mix of the other farming types. Typical combinations are 1+6/7 or 5+6.

**Activity profile**
```yaml
tillage_cultivation: main
planting_seeding: main
crop_care: main
fertilizing: main
irrigation: secondary
harvest: outsourced_main
barn_management: main
feeding: main
milking: main
slurry_handling: main
storing: main
sorting_packing: secondary
moving_transport: main
cleaning: main
```

**Interpretation**
- Broadest operational footprint of all farm types.
- Combines field and livestock activity in one business.
- Often includes both crop-production workflows and animal-care workflows.
- Harvest remains important and may be outsourced.

## Cross-type patterns

### Crop-dominant farm types
These are primarily crop-oriented:
- TF1 field crops
- TF2 horticulture
- TF3 wine
- TF4 other permanent crops

Shared pattern:
- strong field activity
- strong harvest and post-harvest handling
- no livestock-management activity

### Livestock-dominant farm types
These are primarily animal-oriented:
- TF5 dairy
- TF6 other grazing livestock
- TF7 granivores

Shared pattern:
- barn_management, feeding, and cleaning matter strongly
- crop activity is limited or absent
- TF5 and TF6 include more land-related support activity than TF7

### Mixed farms
- TF8 combines both crop and livestock patterns
- useful default assumption when a farm appears operationally broad

## Agent-use rules

### 1. Infer likely needs from farm type
- Crop-heavy types are more likely to need help with cultivation, crop care, irrigation, harvest, storage, packing, and transport.
- Livestock-heavy types are more likely to need help with barn systems, feeding, slurry handling, cleaning, and internal operations.
- Mixed farms may need both.

### 2. Treat outsourced harvest carefully
For TF1, TF5, TF6, and TF8, harvest is marked as important but likely outsourced.
This means:
- harvest equipment may still matter,
- but contractor-related workflows may be relevant,
- ownership assumptions should be made carefully.

### 3. Do not assume all farms have all activity types
The diagrams are meant to distinguish operational profiles.
The agent should avoid suggesting:
- livestock solutions to crop-only farms,
- crop-field solutions to granivore farms,
- milking-related solutions outside dairy.

## Compact machine-readable summary
```yaml
farm_types:
  TF1:
    name: Field crops
    category: crop
    activities:
      tillage_cultivation: main
      planting_seeding: main
      crop_care: main
      fertilizing: main
      irrigation: main
      harvest: outsourced_main
      barn_management: none
      feeding: none
      milking: none
      slurry_handling: none
      storing: main
      sorting_packing: main
      moving_transport: main
      cleaning: main

  TF2:
    name: Horticulture indoor_outdoor
    category: crop
    activities:
      tillage_cultivation: main
      planting_seeding: main
      crop_care: main
      fertilizing: main
      irrigation: main
      harvest: main
      barn_management: none
      feeding: none
      milking: none
      slurry_handling: none
      storing: main
      sorting_packing: main
      moving_transport: main
      cleaning: main

  TF3:
    name: Wine
    category: crop
    activities:
      tillage_cultivation: main
      planting_seeding: secondary
      crop_care: main
      fertilizing: main
      irrigation: main
      harvest: main
      barn_management: none
      feeding: none
      milking: none
      slurry_handling: none
      storing: main
      sorting_packing: main
      moving_transport: main
      cleaning: main

  TF4:
    name: Other permanent crops
    category: crop
    activities:
      tillage_cultivation: secondary
      planting_seeding: secondary
      crop_care: main
      fertilizing: main
      irrigation: main
      harvest: main
      barn_management: none
      feeding: none
      milking: none
      slurry_handling: none
      storing: main
      sorting_packing: main
      moving_transport: main
      cleaning: main

  TF5:
    name: Dairy
    category: livestock
    activities:
      tillage_cultivation: secondary
      planting_seeding: secondary
      crop_care: secondary
      fertilizing: main
      irrigation: secondary
      harvest: outsourced_main
      barn_management: main
      feeding: main
      milking: main
      slurry_handling: main
      storing: main
      sorting_packing: none
      moving_transport: main
      cleaning: main

  TF6:
    name: Other grazing livestock
    category: livestock
    activities:
      tillage_cultivation: secondary
      planting_seeding: secondary
      crop_care: secondary
      fertilizing: main
      irrigation: secondary
      harvest: outsourced_main
      barn_management: main
      feeding: main
      milking: none
      slurry_handling: main
      storing: main
      sorting_packing: none
      moving_transport: main
      cleaning: main

  TF7:
    name: Granivores
    category: livestock
    activities:
      tillage_cultivation: none
      planting_seeding: none
      crop_care: none
      fertilizing: none
      irrigation: none
      harvest: none
      barn_management: main
      feeding: main
      milking: none
      slurry_handling: main
      storing: main
      sorting_packing: none
      moving_transport: secondary
      cleaning: main

  TF8:
    name: Mixed
    category: mixed
    activities:
      tillage_cultivation: main
      planting_seeding: main
      crop_care: main
      fertilizing: main
      irrigation: secondary
      harvest: outsourced_main
      barn_management: main
      feeding: main
      milking: main
      slurry_handling: main
      storing: main
      sorting_packing: secondary
      moving_transport: main
      cleaning: main
```


---

## Machine usage layer

### Purpose
This section adds likely machine usage by farming-type cluster and season.

### Season legend
- `spring`
- `summer`
- `autumn`
- `winter`

### Machine usage structure
The source groups machines into three buckets:
1. machines related to **crop growing** (`TF1`, `TF2`, `TF3`, `TF4`, `TF8`)
2. machines related to **livestock farming** (`TF5`, `TF6`, `TF7`, `TF8`)
3. machines used across **multiple farming types**

## Machines related to crop growing
**Applicable farm types:** `TF1`, `TF2`, `TF3`, `TF4`, `TF8`

```yaml
crop_growing_machines:
  applicable_farm_types: [TF1, TF2, TF3, TF4, TF8]

  power_tractor:
    compact:
      seasons: [spring, summer, autumn, winter]
    medium_big:
      seasons: [spring, summer, autumn, winter]

  tillage_and_seeding:
    ploughing:
      seasons: [spring, autumn]
    tillage:
      seasons: [spring, autumn]
    seeding_and_planting:
      seasons: [spring, autumn]

  crop_care_fertilizing:
    fertilizers:
      seasons: [spring, summer]
    sprayers:
      seasons: [spring, summer]
    mechanical_weeding:
      seasons: [spring, summer]

  irrigation:
    reel_systems_pivot_drips:
      seasons: [spring, summer]

  harvest:
    combines_and_root_crop_harvesters:
      seasons: [summer]
    grape_harvesters_tree_shakers:
      seasons: [summer]
```

### Interpretation
- Crop-growing types need tractor power across the full year.
- Tillage and planting equipment is concentrated in **spring** and **autumn**.
- Fertilizing, spraying, weeding, and irrigation are mostly **spring/summer**.
- Harvest machines are concentrated in **summer** in the source visual.

## Machines related to livestock farming
**Applicable farm types:** `TF5`, `TF6`, `TF7`, `TF8`

```yaml
livestock_machines:
  applicable_farm_types: [TF5, TF6, TF7, TF8]

  power_tractor:
    medium:
      seasons: [spring, summer, autumn, winter]

  feeding:
    silage_cutter:
      seasons: [winter]
    feeder_mixer:
      seasons: [winter]

  fertilizing:
    fertilizers:
      seasons: [spring, summer]
    slurry_manure:
      seasons: [spring, summer, autumn]

  haymaking:
    mowers:
      seasons: [spring, summer, autumn]
    tedders_rakes:
      seasons: [spring, summer, autumn]
    hay_forage_harvesters:
      seasons: [spring, summer, autumn]

  harvest:
    balers:
      seasons: [spring, summer, autumn]
    pick_up_wagons:
      seasons: [spring, summer, autumn]
```

### Interpretation
- Livestock-related farm types still use tractors year-round.
- Feeding equipment is especially associated with **winter**.
- Slurry/manure handling spans **spring to autumn**.
- Haymaking and forage-harvest equipment is concentrated outside winter.

## Other machines used across multiple farming types
**Applicable scope:** broad cross-type usage

```yaml
cross_type_machines:
  transport:
    universal_trailer:
      seasons: [spring, summer, autumn]
    universal_wagon:
      seasons: [spring, summer, autumn]

  cleaning:
    rotary_brush:
      seasons: [spring, summer, autumn, winter]
    high_pressure_water:
      seasons: [spring, summer, autumn, winter]

  internal_transport:
    forklift:
      seasons: [spring, summer, autumn, winter]

  material_handling:
    telehandler:
      seasons: [spring, summer, autumn, winter]
    wheel_loader:
      seasons: [spring, summer, autumn, winter]
    front_loader:
      seasons: [spring, summer, autumn, winter]
```

### Interpretation
- Transport equipment is mainly non-winter in the source.
- Cleaning, internal transport, and material-handling machines are relevant all year.
- These are good default machine categories when farm type is broad or mixed.

## Agent-use mapping from farm type to likely machines

### TF1 — Field crops
Prioritize:
- medium/big tractors
- ploughing, tillage, seeding and planting
- fertilizers, sprayers, mechanical weeding
- irrigation systems where relevant
- combines and root-crop harvesters
- universal trailers / wagons
- cleaning and material handling as secondary support

### TF2 — Horticulture
Prioritize:
- compact and medium tractors depending on scale
- seeding and planting
- crop care tools, fertilizing, spraying, mechanical weeding
- irrigation systems
- transport, sorting-flow support, and cleaning equipment
- material handling for internal movement

### TF3 — Wine
Prioritize:
- compact tractors
- crop care and spraying
- fertilizing
- irrigation where relevant
- grape harvesters / tree shakers
- transport and cleaning support equipment

### TF4 — Other permanent crops
Prioritize:
- compact tractors
- crop care and spraying
- fertilizing
- irrigation
- grape-harvester / tree-shaker-like harvest machinery category for orchard/permanent-crop harvesting
- transport and cleaning support equipment

### TF5 — Dairy
Prioritize:
- medium tractors
- feeder mixers and silage cutters
- fertilizers and slurry/manure handling
- mowers, tedders/rakes, hay and forage harvesters
- balers and pick-up wagons
- telehandlers, wheel-loaders, front-loaders
- high-pressure water and rotary brush cleaning

### TF6 — Other grazing livestock
Prioritize:
- medium tractors
- fertilizers and slurry/manure handling
- haymaking and forage machinery
- balers and pick-up wagons
- telehandlers / wheel-loaders / front-loaders
- cleaning equipment

### TF7 — Granivores
Prioritize:
- medium tractors where site logistics require them
- internal transport and material handling
- feeding-related handling logic
- slurry/manure handling
- forklift, telehandler, wheel-loader, front-loader
- high-pressure water and rotary brush cleaning

### TF8 — Mixed
Prioritize both crop-growing and livestock machine groups:
- tractors of multiple sizes
- tillage/seeding/crop-care machinery
- feeding and slurry/manure systems
- haymaking and harvest machinery
- transport, material handling, and cleaning equipment

## Compact machine-readable add-on
```yaml
machine_usage_by_cluster:
  crop_growing:
    farm_types: [TF1, TF2, TF3, TF4, TF8]
    machines:
      compact_tractor: [spring, summer, autumn, winter]
      medium_big_tractor: [spring, summer, autumn, winter]
      ploughing: [spring, autumn]
      tillage: [spring, autumn]
      seeding_planting: [spring, autumn]
      fertilizers: [spring, summer]
      sprayers: [spring, summer]
      mechanical_weeding: [spring, summer]
      irrigation_systems: [spring, summer]
      combines_root_crop_harvesters: [summer]
      grape_harvesters_tree_shakers: [summer]

  livestock:
    farm_types: [TF5, TF6, TF7, TF8]
    machines:
      medium_tractor: [spring, summer, autumn, winter]
      silage_cutter: [winter]
      feeder_mixer: [winter]
      fertilizers: [spring, summer]
      slurry_manure: [spring, summer, autumn]
      mowers: [spring, summer, autumn]
      tedders_rakes: [spring, summer, autumn]
      hay_forage_harvesters: [spring, summer, autumn]
      balers: [spring, summer, autumn]
      pick_up_wagons: [spring, summer, autumn]

  cross_type:
    machines:
      universal_trailer: [spring, summer, autumn]
      universal_wagon: [spring, summer, autumn]
      rotary_brush: [spring, summer, autumn, winter]
      high_pressure_water: [spring, summer, autumn, winter]
      forklift: [spring, summer, autumn, winter]
      telehandler: [spring, summer, autumn, winter]
      wheel_loader: [spring, summer, autumn, winter]
      front_loader: [spring, summer, autumn, winter]
```

## Combined decision rule for agents
When farm type is known:
1. use the farm-type activity profile to infer **what work is being done**
2. use the machine layer to infer **which machine categories are likely relevant**
3. use seasonality to infer **when those machines are most likely needed**

Examples:
- `TF3` + summer -> likely crop-care / vineyard operations and grape-harvest-related machinery
- `TF5` + winter -> likely feeding, barn operations, cleaning, and feeding equipment
- `TF8` + spring -> both crop establishment and livestock-support machinery may be relevant
