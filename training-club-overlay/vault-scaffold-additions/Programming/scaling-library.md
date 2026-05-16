---
type: scaling-library
generated_by: claude-code
created: YYYY-MM-DD
updated: YYYY-MM-DD
---

# Scaling Library — [CLUB_NAME]

> Every scaling rule the club uses, organized by HYROX station. The `block-builder` skill pulls from this when [PARTNER_NAME] asks for scaling on a workout. Update when the club adopts a new scaling pattern.

---

## SkiErg (1000m)

- **Pro:** 1000m at race pace (sub-4:00 men / sub-4:30 women target)
- **RX:** 1000m, no pace target
- **Scaled:** 500m
- **Shoulder-flagged:** Substitute 1000m bike erg

---

## Sled Push (50m)

- **Pro:** 1.5x bodyweight load
- **RX:** 1x bodyweight load
- **Scaled:** 0.5x bodyweight, may split into 25m + 25m with 30s rest
- **Knee-flagged:** Substitute heavy farmer carries (50m)

---

## Sled Pull (50m)

- **Pro:** 1x bodyweight, hand-over-hand
- **RX:** 0.75x bodyweight
- **Scaled:** 0.5x bodyweight, may use both hands together
- **Shoulder-flagged:** Substitute KB rows (3x10)

---

## Burpee Broad Jumps (80m)

- **Pro:** Full burpee, max-distance broad jump, target 80m
- **RX:** Burpee + 1m step jump (no max distance pressure)
- **Scaled:** Squat thrust + 1m step (no chest-to-floor required)
- **Lower-back-flagged:** Substitute 80 lunges

---

## Rowing (1000m)

- **Pro:** 1000m at race pace
- **RX:** 1000m, no pace target
- **Scaled:** 500m
- **Lower-back-flagged:** Substitute bike erg 1000m

---

## Farmer's Carry (200m)

- **Pro:** 24kg / 16kg kettlebells per hand, 200m unbroken
- **RX:** 20kg / 12kg per hand
- **Scaled:** 16kg / 8kg per hand, may break into 100m + 100m with 30s rest
- **Grip-flagged:** Substitute heavy backpack carry

---

## Sandbag Lunges (100m)

- **Pro:** 30kg / 20kg sandbag, 100m
- **RX:** 20kg / 12kg sandbag
- **Scaled:** Bodyweight lunges 100m
- **Knee-flagged:** Substitute step-ups 100 reps

---

## Wall Balls

- **Pro:** Standard target (10ft men / 9ft women), 9kg / 6kg ball, men 100 reps / women 75 reps
- **RX:** Standard target, 6kg / 4kg ball
- **Scaled:** Lower target by 6 inches OR substitute med-ball squat with overhead reach
- **Shoulder-flagged:** Substitute weighted goblet squats (no overhead)

---

## How to use this library

When the `block-builder` skill is asked for scaling, it:

1. Identifies the station in the workout
2. Pulls the relevant section above
3. Surfaces all four tiers (Pro / RX / Scaled / injury-flagged)
4. Asks [PARTNER_NAME] which tier(s) to publish for the day's class

When the club adopts a new scaling rule:

1. [PARTNER_NAME] says *"add to scaling library: [new rule]"*
2. AI proposes the addition in the right station section
3. [PARTNER_NAME] confirms, AI appends, bumps `updated:` frontmatter

## Customization for [CLUB_NAME]

This is a starter library. Customize during kick-off Section C or anytime by saying *"update the scaling library — [rule]."* The defaults above are standard HYROX scalings; your club may have its own variations.
