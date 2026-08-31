# Basic DCS Mission Editor

---
## General Knowledge:

- Missions folder: C:/Users/You/Saved Games/DCS/Missions/*.miz;
- Every mission is saved as .miz file that stores all external files (.ogg, .jpg) used in the mission. If you rename that extension to .zip, you can access its content;
- Through the left sidebar menu, Triggers have their own window where you can see all of them listed in a row;
    - Triggers column = you define a descriptive name and then the trigger type (that is not so intuitive what each means);
    - Conditions column = as the name suggests!
    - Actions column = as the name suggests!
- DCS mission editor is strongly based on boolean values called "Flags";
    - A "Flag" accepts just an integer as its value;
    - [Take note of each flag like this](https://docs.google.com/spreadsheets/d/11NXuQpOen83lJCSYH6cVF2Q8_GuFNDRTr8FFaEXb48U/edit?gid=0#gid=0). Even if typing the flag number in the trigger name looks good, it's not enough when you face logical questions;
- Player Group/unit name:
    - Group: Flight-A (logic on briefing enlistment).
        - Every unit: PLAYER-`PLANEMODEL`-A1 (easier to find in dropdown menus in triggers)
- Without a Lua script, you cannot spawn and despawn the same group repeatedly. "Group Deactivate" during the match means "to delete" that group, unfortunately;
- To save server performance, use "Group AI on/off" options, and for your information, DCS doesn't use any kind of Dynamic Activation like Arma, so an AI 150km far from the nearest player will use the same CPU as that AI with the player. So use Group AI on/off as much as needed.
- In the triggers list at the bottom, there is a "Initialization Script" field. The Initialization Script field in the DCS World Mission Editor executes Lua code before the mission environment completely loads and before any trigger conditions or standard triggers run;
- Custom Kneeboard pages: rename the .miz to .zip, extract it to a folder, create this path in uppercase (KNEEBOARD/IMAGE/). For each image, use number + underscore + custom description like: 01_overview, 02_routes, etc.

---
## What is the Trigger name logic I like to follow:

[https://i.ibb.co/jkyZ0PP3/image.png](https://i.ibb.co/jkyZ0PP3/image.png)
[https://i.ibb.co/jZ1YpTwr/image.png](https://i.ibb.co/jZ1YpTwr/image.png)
[https://i.ibb.co/Gf7RFXLd/image.png](https://i.ibb.co/Gf7RFXLd/image.png)
[https://i.ibb.co/cSsbJ9zH/image.png](https://i.ibb.co/cSsbJ9zH/image.png)
- If the trigger calls a flag creation ("Flag on"), this trigger name must be "Flag XXX: ....";
- Trigger color only for those about "Mission Status" (win, neutral, fail);
    - Use "blue" for triggers that need to be tested or have an issue;

## Trigger types column:

- **Type: Mission Start**
    - It checks its condition just once;
    - It's automatically deleted right after its condition is checked, no matter the result;
- **Type: Once**
    - It checks its condition 1x per second;
    - It's automatically deleted only when its condition is completely true;
- **Type: Repetitive Action**
    - It checks its condition 1x per second;
    - It's never deleted, no matter the condition result;
    - While its condition is true, it will repeatedly execute its actions;
    - If its condition becomes completely false again, the trigger stays working, waiting until the true condition;
- **Type: Switched Condition**
    - It checks its condition 1x per second;
    - It's never deleted, no matter the condition result;
    - When its condition is completely true, it executes its actions just once;
    - Since it's never deleted, once true, it enters an idle state until the mission ends or it has its condition dynamically changed by another trigger;

## Trigger Conditions column options:

- Time More = ==xxxxx==
    - It doesn't work with "Mission Start" trigger type;
- Time Less = ==xxxxx==
- Time Since Flag = Perfect when you wanna add action(s) delay case a specific flag is true;
- Flag is True = If a flag exists, this condition is true;
- Flag is False = If a flag doesn't exist, this condition is true;
- Unit Alive = ==xxxxx==
- Group Dead = ==xxxxx==
- Random = Add a probability to be considered and commonly you will use a flag action or group activation;
    - This just works with "Mission Start" trigger type.

## Trigger Actions column options:

- Do Script file = load (and auto copy) any Lua file anywhere in your local machine each time the mission is saved.
- Flag On = Create a flag using any integer (number) only.
- Flag Set Random Value = ==xxxxx==.
- Group Activate = Once an object/group is checked with 'Late Activation", this action will activate the group.
- Set Briefing = You update the "Objective" area in the Briefing Screen.

## Airplane Task options:

- **Air-to-Air Roles**
    - CAP (Combat Air Patrol): Defensive or area-control role. AI patrols an assigned area and engages any enemy aircraft detected within their detection/radar envelope.
    - Fighter Sweep: Offensive air superiority. AI actively hunts enemy aircraft ahead of friendly bomber waves or deep behind enemy lines.
    - Escort: Dedicated protection. AI stays close to a designated friendly asset (like a flight of B-17s) and only engages hostiles that threaten the escorted flight.
    - Intercept: Quick-scramble air defense. AI focuses on vectoring straight to incoming hostiles (typically enemy bombers or reconnaissance) to destroy them before they reach their targets.
- **Air-to-Ground Roles**
    - CAS (Close Air Support): Tactical ground attack near friendly troops. AI targets light vehicles, artillery, and infantry. Highly useful for Jabos (like Fw 190 A-8s or P-47s) supporting frontline ground battles.
    - Ground Attack: Direct strike against fixed structures, supply lines, soft targets, or fortified positions (e.g., train yards, encampments, supply depots).
    - Runway Attack: Dedicated strike mission targeting enemy airfields to destroy runways and grounded aircraft.
    - Pinpoint Strike: High-precision bombing against specific individual high-value targets (bridges, radar towers, bunker command posts).
    - Anti-Ship: Maritime strike targeting convoys, landing craft, or naval vessels.
- **Support & Utility Roles**
    - Reconnaissance: Flying a path to gather intelligence. AI avoids direct engagements unless attacked.
    - Transport / Aerobatics / Nothing: Utility tasks typically used to set up civil flights, unarmed utility drops, or customized AI scripts without default combat behaviors.

## Airplane Reaction To Threat options:

- No Reaction: Ignores threats and performs no defensive reaction. It won't maneuver to evade, use defensive countermeasures as a threat response, or abort because of the threat.
- Passive Defense: Uses defensive systems such as chaff/flares/ECM, but does not perform evasive maneuvers.
- Evade Fire: Performs defensive maneuvers when threatened, and also uses passive defenses.
- Allow Abort Mission: The most permissive/default behavior: if the AI considers the threat sufficiently dangerous, it can abort its mission and RTB.
- Horizontal AAA fire evade: ==xxxxx==.