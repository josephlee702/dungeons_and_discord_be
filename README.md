# Dungeons & Discord (Back End) - Project README
# Back-End

Link to [](https://consultancy-fe-b49461b80f89.herokuapp.com/)<br>
Link to [DnD 5e API](https://5e-bits.github.io/docs/)<br>
Link to [Front End Service](https://github.com/aevans27/Dungeons-and-Discord-FE)

---

## Setup
- Ruby 3.2.2
- Rails 7.0.7.2
- [Faraday](https://github.com/lostisland/faraday) A gem to interact with APIs
- [SimpleCov](https://github.com/simplecov-ruby/simplecov) A gem for code coverage tracking
- [ShouldaMatchers](https://github.com/thoughtbot/shoulda-matchers) A gem for testing assertions
- [VCR](https://github.com/vcr/vcr) / [Webmock](https://github.com/bblimke/webmock) Both utilized to stub HTTP requests in tests to simulate API interactions
- [Omniauth](https://github.com/omniauth/omniauth) A gem for Oauth 

## Project Description
Tired of having to lug around a sheet of paper with all of characters attributes for your Dungeons and Dragons games? You get all the way to the Dungeon Master's lair and forgot your character sheet? Cry no longer, weary traveler, **Dungeons and Discord** is here! Utilizing Discord to log in to the app, users are able to create characters by naming the character and selecting a class. Once the character has been created, this character is stored for you, so you don't have to remember that pesky piece of paper again! Players can also utilize Discord's server creation so a DM can host a game over the voice channel and a session can happen from the comfort of your home, car, anywhere with stable connection to the internet!

This repository provides the back end of the project, utilizing the external API calls from the [Dungeons and Dragons 5e API](https://5e-bits.github.io/docs/), it also handles data storage for all the aspects of a Character in DnD.


## Database Schema
```
  create_table "characters", force: :cascade do |t|
    t.integer "user_id"
    t.string "name"
    t.string "char_class"
    t.string "subclass"
    t.integer "level"
    t.string "race"
    t.string "background"
    t.string "alignment"
    t.integer "experience_points"
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
  end

 create_table "character_stats", force: :cascade do |t|
    t.bigint "character_id", null: false
    t.integer "str"
    t.integer "dex"
    t.integer "con"
    t.integer "int"
    t.integer "wis"
    t.integer "cha"
    t.integer "armor_class"
    t.integer "max_hit_point"
    t.integer "current_hit_points"
    t.integer "speed"
    t.datetime "created_at", null: false
    t.datetime "updated_at", null: false
    t.index ["character_id"], name: "index_character_stats_on_character_id"
  end
  ```

## Endpoints


1. `GET /api/v1/characters/{character_id}`
Note: A character must be created on the Front End of the app in order to have a character id. This response would contain ALL of the charcters in the database, regardless of which user it is associated with. This example only contains one character.
_Example Response:_
```
{
    "data": {
        "id": "1",
        "type": "character",
        "attributes": {
            "id": 1,
            "user_id": 1,
            "char_class": "barbarian",
            "race": "half-orc",
            "alignment": "chaotic good",
            "background": "Acolyte",
            "name": "Shrek",
            "character_proficiencies": [
                {
                    "id": 1,
                    "character_id": 1,
                    "proficiency_name": "Light Armor",
                    "created_at": "2024-01-12T02:24:06.849Z",
                    "updated_at": "2024-01-12T02:24:06.849Z"
                },
                {
                    "id": 2,
                    "character_id": 1,
                    "proficiency_name": "Medium Armor",
                    "created_at": "2024-01-12T02:24:06.858Z",
                    "updated_at": "2024-01-12T02:24:06.858Z"
                },
                {
                    "id": 3,
                    "character_id": 1,
                    "proficiency_name": "Shields",
                    "created_at": "2024-01-12T02:24:06.861Z",
                    "updated_at": "2024-01-12T02:24:06.861Z"
                },
                {
                    "id": 4,
                    "character_id": 1,
                    "proficiency_name": "Simple Weapons",
                    "created_at": "2024-01-12T02:24:06.864Z",
                    "updated_at": "2024-01-12T02:24:06.864Z"
                },
                {
                    "id": 5,
                    "character_id": 1,
                    "proficiency_name": "Martial Weapons",
                    "created_at": "2024-01-12T02:24:06.867Z",
                    "updated_at": "2024-01-12T02:24:06.867Z"
                },
                {
                    "id": 6,
                    "character_id": 1,
                    "proficiency_name": "Saving Throw: STR",
                    "created_at": "2024-01-12T02:24:06.869Z",
                    "updated_at": "2024-01-12T02:24:06.869Z"
                },
                {
                    "id": 7,
                    "character_id": 1,
                    "proficiency_name": "Saving Throw: CON",
                    "created_at": "2024-01-12T02:24:06.872Z",
                    "updated_at": "2024-01-12T02:24:06.872Z"
                },
                {
                    "id": 8,
                    "character_id": 1,
                    "proficiency_name": "Skill: Animal Handling",
                    "created_at": "2024-01-12T02:24:06.874Z",
                    "updated_at": "2024-01-12T02:24:06.874Z"
                },
                {
                    "id": 9,
                    "character_id": 1,
                    "proficiency_name": "Skill: Intimidation",
                    "created_at": "2024-01-12T02:24:06.876Z",
                    "updated_at": "2024-01-12T02:24:06.876Z"
                }
            ],
            "character_items": [
                {
                    "id": 1,
                    "character_id": 1,
                    "item_name": "Explorer's Pack",
                    "created_at": "2024-01-12T02:24:13.908Z",
                    "updated_at": "2024-01-12T02:24:13.908Z"
                },
                {
                    "id": 2,
                    "character_id": 1,
                    "item_name": "Javelin",
                    "created_at": "2024-01-12T02:24:13.915Z",
                    "updated_at": "2024-01-12T02:24:13.915Z"
                },
                {
                    "id": 3,
                    "character_id": 1,
                    "item_name": "Greataxe",
                    "created_at": "2024-01-12T02:24:13.918Z",
                    "updated_at": "2024-01-12T02:24:13.918Z"
                },
                {
                    "id": 4,
                    "character_id": 1,
                    "item_name": "Handaxe",
                    "created_at": "2024-01-12T02:24:13.920Z",
                    "updated_at": "2024-01-12T02:24:13.920Z"
                }
            ],
            "character_stat": {
                "id": 1,
                "character_id": 1,
                "str": 9,
                "dex": 2,
                "con": 6,
                "int": 10,
                "wis": 3,
                "cha": 20,
                "armor_class": null,
                "max_hit_point": 12,
                "current_hit_points": null,
                "speed": null,
                "created_at": "2024-01-12T02:24:36.422Z",
                "updated_at": "2024-01-12T02:24:36.422Z"
            }
        }
    }
}

```

2. `GET /api/v1/charclasses/add_items`
Note: This response happens once a New Character creation has begun. This 
_Example Response:_
```
{
    "data": {
        "id": null,
        "type": "charclass",
        "attributes": {
            "id": null,
            "index": null,
            "name": null,
            "hit_die": null,
            "proficiency_choices": null,
            "proficiencies": null,
            "saving_throws": null,
            "starting_equipment": null,
            "starting_equipment_options": null,
            "subclass": null
        }
    }
}
```

3. `GET http://localhost:3000/api/v1/charclasses/wizard`
Note: This response is being called in the front end when the first step of creating a character is made when selecting a Name and a DnD Class from a drop down menu. This example call is making the Wizard class as a selection.
_Example Response:_
```
{
    "data": {
        "id": null,
        "type": "charclass",
        "attributes": {
            "id": null,
            "index": "wizard",
            "name": "Wizard",
            "hit_die": 6,
            "proficiency_choices": [
                {
                    "desc": "Choose two from Arcana, History, Insight, Investigation, Medicine, and Religion",
                    "choose": 2,
                    "type": "proficiencies",
                    "from": {
                        "option_set_type": "options_array",
                        "options": [
... continued but a very long response ...
                }
            ]
        }
    }
}

```
4. `GET /api/v1/equipment/martial-melee-weapons` 
Note: this response is not utilized in the Front End currently, but lists possible choices of every Martial Melee Weapon. 
_Example Response:_
```
{
    "data": [
        {
            "id": null,
            "type": "equipment",
            "attributes": {
                "index": "battleaxe",
                "name": "Battleaxe"
            }
        },
        {
            "id": null,
            "type": "equipment",
            "attributes": {
                "index": "flail",
                "name": "Flail"
            }
        },
        {
   ... continued but a very long response ...
        },
        {
            "id": null,
            "type": "equipment",
            "attributes": {
                "index": "warhammer",
                "name": "Warhammer"
            }
        },
        {
            "id": null,
            "type": "equipment",
            "attributes": {
                "index": "whip",
                "name": "Whip"
            }
        }
    ]
}

```



## Contributors

- [Paul Bennett](https://www.linkedin.com/in/paul-bennett-dev/) -GitHub: [@pcbennett108](https://github.com/pcbennett108)
- [Allan Evans](https://www.linkedin.com/in/allan-evans-2c/) - GitHub: [@aevans27](https://github.com/aevans27)
- [Xander Hendry](https://www.linkedin.com/in/xander-hendry-70b804289/) - GitHub: [@XanderHendry](https://github.com/XanderHendry)
- [Joseph Lee](https://www.linkedin.com/in/joseph-lee702/) - GitHub: [@josephlee702](https://github.com/josephlee702)
- [Cory Powell](https://www.linkedin.com/in/coryrpow/) - GitHub: [@coryrpow](https://github.com/coryrpow)
