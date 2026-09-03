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

## `Trigger types` column:

- **Type:** <span style="color: white; background-color: green; padding:0 5px;">Mission Start</span>
    - It checks its condition just once;
    - It's automatically deleted right after its condition is checked, no matter the result;
- **Type:** <span style="color: white; background-color: green; padding:0 5px;">Once</span>
    - It checks its condition 1x per second;
    - It's automatically deleted only when its condition is completely true;
- **Type:** <span style="color: white; background-color: green; padding:0 5px;">Repetitive Action</span>
    - It checks its condition 1x per second;
    - It's never deleted, no matter the condition result;
    - While its condition is true, it will repeatedly execute its actions;
    - If its condition becomes completely false again, the trigger stays working, waiting until the true condition;
- **Type:** <span style="color: white; background-color: green; padding:0 5px;">Switched Condition</span>
    - It checks its condition 1x per second;
    - It's never deleted, no matter the condition result;
    - When its condition is completely true, it executes its actions just once;
    - Since it's never deleted, once true, it enters an idle state until the mission ends or it has its condition dynamically changed by another trigger;

## `Trigger Conditions` column options:

- <span style="color: white; background-color: green; padding:0 5px;">Time More</span> = ==xxxxx==
    - It doesn't work with "Mission Start" trigger type;
- <span style="color: white; background-color: green; padding:0 5px;">Time Less</span> = ==xxxxx==
- <span style="color: white; background-color: green; padding:0 5px;">Time Since Flag</span> = Perfect when you wanna add action(s) delay case a specific flag is true;
- <span style="color: white; background-color: green; padding:0 5px;">Flag is True</span> = If a flag exists, this condition is true;
- <span style="color: white; background-color: green; padding:0 5px;">Flag is False</span> = If a flag doesn't exist, this condition is true;
- <span style="color: white; background-color: green; padding:0 5px;">Unit Alive</span> = ==xxxxx==
- <span style="color: white; background-color: green; padding:0 5px;">Group Dead</span> = ==xxxxx==
- <span style="color: white; background-color: green; padding:0 5px;">Random</span> = Used only with the trigger type `Start Mission`, it adds a probability to return `True`. If it's true, generally it uses a `Flag On` action and/or a `Group Activation`;
    - This just works with "Mission Start" trigger type.

## `Trigger Actions` column options:

- <span style="color: white; background-color: green; padding:0 5px;">AI Task Set</span> = Replaces the group's current task by another one listed in the group's `Triggered Actions` tab. When this action is called, it's like "Stop doing what you're doing and do this instead".
- <span style="color: white; background-color: green; padding:0 5px;">AI Task Push</span> = Temporarily adds the selected task (listed in the group's `Triggered Actions` tab) on top of the current task. When this action is called, it's like "Do this additional task now, then return to what you were doing".
- <span style="color: white; background-color: green; padding:0 5px;">Do Script file</span> = load (and auto copy) any Lua file anywhere in your local machine each time the mission is saved.
- <span style="color: white; background-color: green; padding:0 5px;">Flag On</span> = Create a flag using any integer (number) only.
- <span style="color: white; background-color: green; padding:0 5px;">Flag Set Random Value</span> = ==xxxxx==.
- <span style="color: white; background-color: green; padding:0 5px;">Group Activate</span> = Once an object/group is checked with 'Late Activation", this action will activate the group.
- <span style="color: white; background-color: green; padding:0 5px;">Set Briefing</span> = You update the "Objective" area in the Briefing Screen.
## What is the differences between actions in a group's `waypoint-0` and those ones in the group's "`Triggered Actions`" tab?

- **Action in `Waypoint-0`:**
	- Make a group behave just like that by default;
	- The group just change it if its `waypoint-1` actions window is not empty;
- **Actions in `Triggered Actions` tab:**
	- All these actions are "planned" to be used dynamically later by mission triggers;
	- Once a group has something in this tab, you can call it using `AI Task Set` and `AI Task Push` through mission triggers;
## Airplane `Task` options:

- **Air-to-Air Roles**
    - <span style="color: white; background-color: green; padding:0 5px;">CAP</span> (Combat Air Patrol): Defensive or area-control role. AI patrols an assigned area and engages any enemy aircraft detected within their detection/radar envelope.
    - <span style="color: white; background-color: green; padding:0 5px;">Fighter Sweep:</span> Offensive air superiority. AI actively hunts enemy aircraft ahead of friendly bomber waves or deep behind enemy lines.
    - <span style="color: white; background-color: green; padding:0 5px;">Escort:</span> Dedicated protection. AI stays close to a designated friendly asset and only engages hostiles that threaten the escorted flight.
    - <span style="color: white; background-color: green; padding:0 5px;">Intercept:</span> Quick-scramble air defense. AI focuses on vectoring straight to incoming hostiles to destroy them before they reach their targets.
- **Air-to-Ground Roles**
    - <span style="color: white; background-color: green; padding:0 5px;">CAS</span> (Close Air Support): Tactical ground attack near friendly troops.
    - <span style="color: white; background-color: green; padding:0 5px;">Ground Attack:</span> Direct strike against fixed structures, supply lines, soft targets, or fortified positions (e.g., train yards, encampments, supply depots).
    - <span style="color: white; background-color: green; padding:0 5px;">Runway Attack:</span> Dedicated strike mission targeting enemy airfields to destroy runways and grounded aircraft.
    - <span style="color: white; background-color: green; padding:0 5px;">Pinpoint Strike:</span> High-precision bombing against specific individual high-value targets (bridges, radar towers, bunker command posts).
    - <span style="color: white; background-color: green; padding:0 5px;">Anti-Ship:</span> Maritime strike targeting convoys, landing craft, or naval vessels.
- **Support & Utility Roles**
    - <span style="color: white; background-color: green; padding:0 5px;">Reconnaissance:</span> Flying a path to gather intelligence. AI avoids direct engagements unless attacked.
    - <span style="color: white; background-color: green; padding:0 5px;">Transport / Aerobatics / Nothing: </span>Utility tasks typically used to set up civil flights, unarmed utility drops, or customized AI scripts without default combat behaviors.

## Airplane `Reaction To Threat` options:

- <span style="color: white; background-color: green; padding:0 5px;">No Reaction:</span> Ignores threats and performs no defensive reaction. It won't maneuver to evade, use defensive countermeasures as a threat response, or abort because of the threat.
- <span style="color: white; background-color: green; padding:0 5px;">Passive Defense:</span> Uses defensive systems such as chaff/flares/ECM, but does not perform evasive maneuvers.
- <span style="color: white; background-color: green; padding:0 5px;">Evade Fire:</span> Performs defensive maneuvers when threatened, and also uses passive defenses.
- <span style="color: white; background-color: green; padding:0 5px;">Allow Abort Mission:</span> The most permissive/default behavior: if the AI considers the threat sufficiently dangerous, it can abort its mission and RTB.
- <span style="color: white; background-color: green; padding:0 5px;">Horizontal AAA fire evade:</span> ==xxxxx==.