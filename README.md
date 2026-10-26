# Longitudinal Control Dialogues

Long-running conversations between the occupants of a space and an assistant that controls the devices in it. Each conversation covers 60 consecutive days, so that preferences stated early can be referred to, revised and relied on later.

Two domains are included: homes and office/school buildings. A third domain (a factory) will be added in the same form.

All turns are requests from occupants, in time order, with the place the occupant is in at the time. The same four-phase design is used in every conversation (days 1–7, 8–20, 21–40, 41–60): occupants first state their preferences explicitly, then refer to them in shortened form, later state competing preferences for the same situation, revise some of them explicitly, and revisit settings after long gaps; ordinary everyday requests run through the whole period. The exact construction and the evaluation protocol are described in the accompanying paper.

## Home domain (`home/`)

Three simulated households.

| Household | Residents | Rooms | Devices | Days | Turns |
|---|---|---|---|---|---|
| home_01 | Ari | 5 | 9 | 60 | 331 |
| home_02 | Ben, Mia | 5 | 9 | 60 | 338 |
| home_03 | Leo, Sara, Nina | 7 | 10 | 60 | 424 |

Residents, rooms, devices and all requests are synthetic.

`home/<household>/household.json`: the residents (name, daily schedule), the rooms, the devices (name, type, room, capabilities, default state) and the scenes.

`home/<household>/dialogues.jsonl`: one line per day (`day` 1–60) with the day's `turns` in time order: `id`, `time` (`HH:MM`), `speaker`, `room`, `utterance`.

## Building domain (`building/`)

Three sites, each run by a small team of facility managers who ask the assistant to operate windows, lighting, plugs, doors, air conditioning and ventilation.

| Site | Setting | Occupants | Areas | Devices | Days | Turns |
|---|---|---|---|---|---|---|
| building_01 | University office building (site 05, five offices) | 3 | 5 | 20 | 60 | 1141 |
| building_02 | Middle-school campus, buildings B and C (site 15, five rooms) | 3 | 5 | 14 | 60 | 425 |
| building_03 | Naturally ventilated office building (site 24, fifteen offices) | 4 | 15 | 18 | 60 | 693 |

`building/<site>/site.json`: the occupants (name, role), the areas, the devices (name, type, area, default state) and the opening hours.

`building/<site>/dialogues.jsonl`: one line per day with the day's `turns`: `id`, `time`, `speaker`, `area`, `utterance`.

The three sites and the timing of their everyday requests are adapted from in-situ occupant behaviour records of three sites (sites 05, 15 and 24) of the ASHRAE Global Occupant Behavior Database:

Dong, B. et al. A global building occupant behavior database. *Scientific Data* 9, 369 (2022). https://doi.org/10.1038/s41597-022-01475-3

The original records are published on figshare (https://doi.org/10.6084/m9.figshare.16920118.v6) and can be queried at https://ashraeobdatabase.com, under the terms stated there. The requests themselves, the facility managers, the device names and all preference-related turns are synthetic.

## Common conventions

- Every day starts from the default device states given in the site or household file; the assistant's memory is never reset.
- `id` is `<site>_d<day>_t<index>` (day and index within the day, both two digits).
- `MANIFEST.json` lists every file with its size, record count and SHA-256.

## License

The dataset is released under the Creative Commons Attribution 4.0 International License (CC BY 4.0); see `LICENSE`.

## Citation

The accompanying paper is under review. The citation will be added here.
