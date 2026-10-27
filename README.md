# Longitudinal Control Dialogues

Long-running conversations between the occupants of a space and an assistant that controls the devices in it. Each conversation covers 60 consecutive days, so that preferences stated early can be referred to, revised and relied on later.

Three domains are included: homes, office/school buildings and a mineral flotation plant.

All turns are requests from occupants, in time order, with the place the occupant is in at the time. The same four-phase design is used in every conversation (days 1–7, 8–20, 21–40, 41–60): occupants first state their preferences explicitly, then refer to them in shortened form, later state competing preferences for the same situation, revise some of them explicitly, and revisit settings after long gaps; ordinary everyday requests run through the whole period. The exact construction and the evaluation protocol are described in the accompanying paper.

## Home domain (`home/`)

Three simulated households.

| Household | Residents | Rooms | Devices | Days | Turns | Scored |
|---|---|---|---|---|---|---|
| home_01 | Ari | 5 | 9 | 60 | 331 | 127 |
| home_02 | Ben, Mia | 5 | 9 | 60 | 338 | 127 |
| home_03 | Leo, Sara, Nina | 7 | 10 | 60 | 424 | 130 |

Residents, rooms, devices and all requests are synthetic.

`home/<household>/household.json`: the residents (name, daily schedule), the rooms, the devices (name, type, room, capabilities, default state) and the scenes.

`home/<household>/dialogues.jsonl`: one line per day (`day` 1–60) with the day's `turns` in time order: `id`, `time` (`HH:MM`), `speaker`, `room`, `utterance`.

## Building domain (`building/`)

Three sites, each run by a small team of facility managers who ask the assistant to operate windows, lighting, plugs, doors, air conditioning and ventilation.

| Site | Setting | Occupants | Areas | Devices | Days | Turns | Scored |
|---|---|---|---|---|---|---|---|
| building_01 | University office building (site 05, five offices) | 3 | 5 | 20 | 60 | 1141 | 69 |
| building_02 | Middle-school campus, buildings B and C (site 15, five rooms) | 3 | 5 | 14 | 60 | 425 | 67 |
| building_03 | Naturally ventilated office building (site 24, fifteen offices) | 4 | 15 | 18 | 60 | 693 | 68 |

`building/<site>/site.json`: the occupants (name, role), the areas, the devices (name, type, area, default state) and the opening hours.

`building/<site>/dialogues.jsonl`: one line per day with the day's `turns`: `id`, `time`, `speaker`, `area`, `utterance`.

The three sites and the timing of their everyday requests are adapted from in-situ occupant behaviour records of three sites (sites 05, 15 and 24) of the ASHRAE Global Occupant Behavior Database:

Dong, B. et al. A global building occupant behavior database. *Scientific Data* 9, 369 (2022). https://doi.org/10.1038/s41597-022-01475-3

The original records are published on figshare (https://doi.org/10.6084/m9.figshare.16920118.v6) and can be queried at https://ashraeobdatabase.com, under the terms stated there. The requests themselves, the facility managers, the device names and all preference-related turns are synthetic.

## Factory domain (`factory/`)

Three scenarios of one mineral flotation plant, each covering a group of flotation columns operated by four shift crews who ask the assistant to set the air-flow and froth-level setpoints of the columns.

| Scenario | Columns | Operators | Areas | Devices | Days | Turns | Scored |
|---|---|---|---|---|---|---|---|
| factory_01 | 01, 02, 03 | 4 | 3 | 6 | 60 | 830 | 63 |
| factory_02 | 04, 05 | 4 | 2 | 4 | 60 | 300 | 53 |
| factory_03 | 06, 07 | 4 | 2 | 4 | 60 | 326 | 53 |

`factory/<scenario>/plant.json`: the operators (name, role), the shift roster, the areas (one per flotation column) and the devices (name, type, area, unit, admissible range, default state).

`factory/<scenario>/dialogues.jsonl`: one line per day with the day's `turns`: `id`, `time`, `speaker`, `area`, `utterance`.

The timing and the target values of the everyday requests are inferred by a fixed rule from the measured air flow and froth level of the seven flotation columns in the public dataset "Quality Prediction in a Mining Process", published on Kaggle by Eduardo Magalhães Oliveira in 2017 under CC0 (https://www.kaggle.com/datasets/edumagalhaes/quality-prediction-in-a-mining-process), between 2017-04-12 and 2017-06-10. The crews, the wording of all requests and all preference-related turns are synthetic.

## Gold labels

`<domain>/<environment>/gold.jsonl`: one line per scored request. `id`; `expect`, either `execute` or `ask`; for `execute`, `action` (`device`, `action`, `params`) and `recall`, the slots that are not in the request and must come from earlier turns; for `ask`, `ask`, the slots to ask about; `habit`, the standing preference the request belongs to.

`<domain>/<environment>/habits.json`: the standing preferences. `id`; `teaching`, the turns that state the preference in full; `correction` (`turn`, `old`, `new`) where the preference is revised.

Slot names are `device`, `device_type`, `area`, `action` and the parameter names used in `params`.

## Common conventions

- Every day starts from the default device states given in the household, site or plant file; the assistant's memory is never reset.
- `id` is `<environment>_d<day>_t<index>` (day and index within the day, both two digits).
- `area` (or `room`) is `null` when the speaker is not in any of the listed areas at the time of the request.
- A day without requests has an empty `turns` list (factory_01 (2), factory_02 (2), factory_03 (2)).
- `MANIFEST.json` lists every file with its size, record count and SHA-256.

## License

The dataset is released under the Creative Commons Attribution 4.0 International License (CC BY 4.0); see `LICENSE`.

## Citation

The accompanying paper is under review. The citation will be added here.
