# Longitudinal Control Dialogues

Long-running conversations between the occupants of a space and an assistant that controls the devices in it. Each conversation covers 60 consecutive days, so that preferences stated early can be referred to, revised and relied on later.

This release contains the home domain. Two further domains (an office building and a factory) will be added in the same form.

## Home domain

Three simulated households. Every turn is a resident's request, in time order, with the room the resident is in.

| Household | Residents | Rooms | Devices | Days | Turns |
|---|---|---|---|---|---|
| home_01 | Ari | 5 | 9 | 60 | 331 |
| home_02 | Ben, Mia | 5 | 9 | 60 | 338 |
| home_03 | Leo, Sara, Nina | 7 | 10 | 60 | 424 |

Residents, rooms, devices and all requests are synthetic.

### Design

Each 60-day conversation runs through four phases: days 1–7, 8–20, 21–40 and 41–60. Residents first state their preferences explicitly (for example a light's brightness and colour temperature in the morning), then refer to them in shortened form ("my usual reading light"). Later, competing preferences for the same situation appear, some preferences are revised explicitly, and settings are revisited after long gaps. Ordinary everyday requests run through the whole period. The exact construction and the evaluation protocol are described in the accompanying paper.

### Files

`home/<household>/household.json`: the residents (name, daily schedule), the rooms, the devices (name, type, room, capabilities, default state) and the scenes. Every day starts from the default states; the assistant's memory is never reset.

`home/<household>/dialogues.jsonl`: one line per day (`day` 1–60) with the day's `turns` in time order:

| Field | Content |
|---|---|
| `id` | Turn identifier: `<household>_d<day>_t<index>` |
| `time` | Time of day, `HH:MM` |
| `speaker` | Resident's name |
| `room` | Room the resident is in |
| `utterance` | What the resident says |

`MANIFEST.json` lists every file with its size, record count and SHA-256.

## License

The dataset is released under the Creative Commons Attribution 4.0 International License (CC BY 4.0); see `LICENSE`.

## Citation

The accompanying paper is under review. The citation will be added here.
