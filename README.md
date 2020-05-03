
# DIRGE

The Distributed Indie RPG Game Executor


* *D*istributed - designed for use in distributed, remote games (like Roll20 or Astral)
* *I*ndie - created for more indie-style games, like Monster of the Week or Fate
* *R*PG - Role Playing Game
* *G*Ming - the tool is for game masters to run their games
* *E*nvironment - its a framework for running games

# Todos
[] Set Up Project
[] Deploy on Heroku 
[] Show Player Page (name, image, etc) with GameList (hardcoded)
[] Select Game from GameList and set state (hardcoded)
[] differentiate between GM and Players
[] GM sends player 1 an image
[] player 1 rolls dice, Player 2 and GM see it
[] Login via Google
[] Serve TestGame (hardcoded)
[] Serve FateGame (hardcoded)
[] Serve TestChars (hardcoded)
[] Serve FateChars (hardcoded)
[] Serve TestMap (hardcoded)
[] Serve FateMap (hardcoded)
[] GM Sets Image
[] GM Sets Map
[] Character Rolls Dice for all to see

http://a.teall.info/mdice/

# API
GET /game/{game-slug}
GET /game/{game-slug}/character/{character-slug}
PUT /game/{game-slug}/image-slot/{image-slot-id} BODY: imageId

# Components

- Server
    - written in GO
- Client
    - written in React
- Plugins

https://dev.to/cishiv/deploying-to-heroku-docker-go-and-react-38hh


- Root
    - Game
        - Id: Int
        - Name: String
        - Slug: String
        - Image: Image
        - SystemDefinition: SystemDefinition
        - GM: Person
        - Players: List<Person>
        - Maps: List<Map>
        - Handouts: List<Handout>
        - PlayerCharacters: List<PCs>
        - NonPlayerCharacters: List<NPCs>
    
    - Map
        - Choice[Background:Image|GoogleMap]
        - Objects: List<MapObject>
        - GridDefinition: GridDefinition

    - MapObject
        - Image
        - Name
        - Description
        - Position
        - PlayerNotes
        - GmNotes

    - Handout
        - Image
        - Name
        - Description
        - PlayerNotes
        - GmNotes

    - SystemDefinition
        - System Name
        - CharacterDefinition


        - Character
            |   - CharacterName: String
            |   - CharacterSlug: String
            |   - CharacterTitle: String
            |   - Description: String
            |   - HairColor: String
            |   - EyeColor: String
            |   - Height: String
            |   - Weight: String
            |   - Age: String
            |   - Notes: String
            |   - Creator: Person
            |   - CreatedDate: Date
            |   - UpdatedDate: Date
            |   - Images: List<Image>
            |- PC
                - PcSystemDefinition
            |- NPC
                - NpcSystemDefinition

        Image
            - Url
            - Choice[Scale OR Dimensions]

        - PcSystemDefinition
            |- PcFateDefinition
            |   - HighConceptAspect:Aspect
            |   - TroubleAspect: Aspect
            |   - Aspect1: Aspect
            |   - Aspect2: Aspect
            |   - Aspect3: Aspect
            |   - AdditionalAspects: List<Aspect>
            |   - Skills: List<SelectedFateSkill>
            |   - Stunts: List<SelectedFateStunt>
            |       
            |- PcMonsterOfTheWeekDefinition
                - Sharp: MotWAttribute
                - Cool: MotWAttribute
                - Charm: MotWAttribute
                - Tough: MotWAttribute
                - Weird: MotWAttribute
                - SelectedPlaybook: MotWPlaybook
                - SelectedMoves: List<MotWMove>
                - SelectedEquipment: List<MotWMove>

            - MotWAttribute
                - MotWAttributeDef
                - Value: Int (-3..+3)

            - MotWAttributeDef
                - Name: String
                - BasicMoves: List<MotWBasicMove>
                - DicePool: DicePool(2 x D6)

            - SelectedFateSkill
                - Ranking
                - FateSkill

            - FateSkill
                - DicePool: DicePool(4 x DFate)
                - Name: String
                - Description: String
                - Overcome: FateMove
                - Attack: FateMove
                - CreateAnAdvantage: FateMove
                - Defend: FateMove
                - Stunts: List<FateStunt>

            - FateMove
                - Description: String
                - Usage: [Never|Rare|Common]

            - Die
                |- DFate
                |- D2
                |- D3
                |- D4
                |- D6
                |- D8
                |- D10
                |- D12
                |- D20
                |- D100

            - DicePool
                - Dice: List<Die>
