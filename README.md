# Bless Skill Tree

Bless Online stances, rotations and skills using simple HTML and CSS.

## GitHub Pages & Jekyll

The GitHub pages are updated automatically when deploying to `master`. This uses Jekyll to build the site after any changes.

Requirements:

- [Ruby 2.5.1](https://www.ruby-lang.org/en/downloads/)
- [Jekyll](https://jekyllrb.com/)

### Setup

```bash
gem install bundler
bundle install
jekyll serve --livereload
```

This will then run on `localhost:4000` and automatically reload when you change any files.

Updating of the site will happen when a push is made to the `master` branch.

## Pull Requests

I'm more than happy for anyone to help out by submitting a pull request! Feel free to fork the repo and make any changes to submit.

If you have any feature requests or have found any bugs/issues, feel free to submit an Issue on the main repo.

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
  cooldown: 30.00
  crowd-control: true
  skill-details:
    - Non-targeting
    - Mana 2.00% + 100 consumption
  skill-descriptions:
    - Reduces Threat by 30% for 5 seconds.
```

Some skills will have the same name and icon, but may have different effects depending on the stance and place in the combo. The easiest thing to do for now is duplicate the skill in `skills.yml` and name it with a different slug. i.e. `distortion-1` making sure to use the new slug in the correct place in the combo. This is a temporary fix whilst I find better ways of dealing with skills that change effect.

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

## JSON Endpoint

The JSON data is put together in `skills.json`. This uses the same Liquid formatting to create the JSON, pulling from the various `.yml` files.

An example of the JSON is:

```json
  {
    "paladin": {
      "skills": [
        {
          "slug": "holy-explosion",
          "name": "Holy Explosion",
          "image": "paladin/holy-explosion.png",
          "cooldown": 30,
          "crowd-control": true,
          "skill-details": [
            "non targeting skill",
            "maximum mana 10.00% + 100 consumption"
          ],
          "skill-descriptions": [
            "Deals 429 damage to enemies within a 5m radius, knocking them back."
          ]
        }
      ],
      "non_stance_skills": [
        "holy-explosion"
      ]
    }
  }
```
