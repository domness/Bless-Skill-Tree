# Bless Skill Tree

Bless Online stances, rotations and skills using simple HTML and CSS.

## GitHub Pages & Jekyll

The GitHub pages are updated automatically when deploying to `master`. This uses Jekyll to build the site after any changes.

## Class Folder Structure

```
 /class_name
  | stances.yml
  | skills.yml
  | rotations.yml
  | non_stance_skills.yml
  | my_stance_1.yml
  | my_stance_2.yml
```

### stances.yml

This contains a list of `slug` and `name` to provide the name of the stance, and the slug that will be used to reference the correct file containing the skills.

```yaml
- slug: dps_1
  name: DPS 1
```

### skills.yml

Skills are the entire set of available skills for a certain class. Anything that uses a skill (i.e. rotations, non-stance skills etc.), will refer to these by their `slug`.

```yaml
- slug: distortion
  name: Distortion
  image: mage/distortion.png
  skill-details:
    - non targeting skill
    - maximum mana 2.00% + 100 consumption
    - time until can be used again 30.00 seconds
  skill-descriptions:
    - Reduces Threat by 30% for 5 seconds.
```

### rotations.yml

The rotations file just lists the name of the rotation and the slug names of the skills in order.

```yaml
- name: Example combo
  skills:
    - branded
    - seekers-devotion
    - retribution
    - verdict
    - sacred-verdict
    - retribution
```

### non_stance_skills.yml

Non-stance skills can be listed just using their slug.

```yaml
- slug: distortion
- slug: blink
- slug: disenchant
- slug: elemental-discharge
- slug: mana-shield
```

### my_stance_1.yml

This file will be the same as one of the stance slugs in `stances.yml`. It lists the starting skills, and their following skills by their `slug`.

```yaml
- slug: strike
  followed:
    - slug: rapid-strike
      followed:
        - slug: chastise
    - slug: verdict
      followed:
        - slug: conviction

- slug: retribution
  followed:
    - slug: verdict
      followed:
        - slug: sacred-verdict
    - slug: execute
      followed:
        - slug: penalize

- slug: branded
  followed:
    - slug: armor-of-insight
    - slug: prayer
    - slug: seekers-devotion
```

These can be repeated if stances were to allow additional combo skills by just adding an extra:

```yaml
followed:
  - slug: sacred-verdict
```
