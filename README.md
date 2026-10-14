[SuitExporter-README.txt](https://github.com/user-attachments/files/33464731/SuitExporter-README.txt)
# Wolverine-model-to-MSM2-suit-converter
If releasing mods utilizing this tool, please credit me.
SUIT EXPORTER 2.4
Wolverine suit folders  ->  Marvel's Spider-Man 2 (PC) .suit files, converted


WHAT IT DOES
  Drop a suit folder (for example extracted\hero\hero_wolverine_battle) and press "Export .suit files".
  A folder in Marvel's Wolverine format is converted first, then packed:
      models     every wearable part (ubermodel parts + mask) is re-rigged onto Peter's / Miles's Spider-Man 2
                 skeleton, refitted to their proportions, and written as one Spider-Man 2 .model built on the
                 template model (looks Default / body / mask are set up). Logan's face and the art reference are left out.
      textures   untiled from the PS5 layout and rewritten as Spider-Man 2 PC textures (main + HD part).
      materials  every Wolverine material is rebuilt as a Spider-Man 2 suit material: a real Spider-Man 2 material on the
                 standard suit shader (hero_spiderman_suit_ggx, e.g. Miles's Encoded suit torso) with its colour, normal and
                 gloss textures swapped for the suit's converted ones. The gloss textures need no change: that shader reads
                 them the same way Wolverine does. The tiling detail maps are switched off with a black detail mask.
                 Logan's skin under the suit (bare arms on the Battle suit and the like) is converted too when the Wolverine
                 game folder is set: its materials and textures are read from the game. A part with no textures at all
                 (the eye lenses of some masks) keeps a template suit material. Wolverine's invisible helper shells
                 (scalp / hair wrap) are left out.
  Output: Suits\<id>\<id>_peter.suit, <id>_miles.suit, <id>_report.txt (with the full conversion log), and the
  converted files in Suits\<id>\converted\.

WHAT IT NEEDS (set under "Conversion...", found automatically when they are in Downloads)
  - Blender 5.x (blender.exe). It runs in the background; no window opens.
  - the luna_engine_io_tools add-on folder (Downloads\luna_engine_io_tools)
  - Peter template: Downloads\adv\peter\hero_spiderman_advanced.model
  - Miles template: Downloads\adv\miles\hero_spiderman_miles_updated.model
  - Spider-Man 2 suit material: found in Downloads\sm2suits (any material on hero_spiderman_suit_ggx; Miles's
    hero_spiderman_miles_encoded_tor.material is picked first). Without it, the template suit's materials are used.
  - optional: Spider-Man 2 texture folders (Downloads\sm2suits and Downloads\adv): texture header details are copied
    from real Spider-Man 2 textures of the same kind
  - optional: extracted Wolverine files laid out by asset path (Downloads\dat1\extracted is found automatically) and
    the Wolverine game folder (PPSA03671-app0; found from Wolverine Tweaks or C:\wolverine\...). Materials and textures
    the suit folder lacks (skin under clothes, shared teeth and eyes, eye lenses borrowed from other suits) are read
    from them, extracted files first.
  - the SM2Convert folder next to SuitExporter.exe

OTHER CHARACTERS (bosses, NPCs, enemies, civilians)
  Any skinned character folder converts the same way as a Logan suit. Extract it with Wolverine Tweaks (Assets tab,
  search e.g. characters/boss/boss_sabretooth, "Extract all shown") and drop the folder here.
  - Heads: "Head models" under Conversion... Auto leaves the head out only for Logan's own suits (hero_wolverine_*,
    hero_logan_*, or any folder with a mask, where his face sits under the mask) and keeps it for everyone else.
  - Only one version of the character is used: alternative versions next to the base one (hair_civ1, hair_teamx next
    to hair), the one-piece model when the separate ubermodel parts are there, skeleton display models, collision
    shapes and posed art models are left out. The report lists each one and why.
  - Hair: Wolverine draws long hair and beards as flat cards with a see-through strand texture; Spider-Man 2 uses
    strand hair (curves the engine draws as thin hairs, coloured root to tip). Each card is turned into strands that run
    along it: the card's coverage texture says where strands are and where they thin out, its root map which end is the
    root. The strands are skinned to the same bones as the card. Their settings (clumping, thickness, gloss, movement)
    are copied from a real Spider-Man 2 hair: set "Hair donor model" to a Spider-Man 2 model with strand hair (Kraven's
    boss_kraven.model is found in Downloads\kraven model). Without a donor the cards are left out.
    Colour: Wolverine takes hair colour from a palette inside its hair shader, which this tool cannot read, so the hair
    material's own colour is used (often a default brown). Set "Hair colour" (#rrggbb, or pick with Browse...) for the
    real one. Roots are drawn darker than tips, as Spider-Man 2's own hair is.
    Tested with Sabretooth: 586 cards became about 960 strands (hair and beard), and the exported models read back
    with their strands in place. Solid fur shells (his collar) stay ordinary meshes.
  - The report lists, for every part, how many bones match a Spider-Man 2 bone and which skinned bones do not.
    Unmatched bones follow their parent: facial bones follow the head (the face does not animate; Peter and Miles
    have no face rig), hair and cloth bones stay still, Peter's lower-leg twist bones follow the knee (Peter's own
    suits have none either). Bodies very different from a person (tentacles, Sentinels) will move stiffly.
  - Materials outside the folder (skin under clothes, shared teeth and eyes) come from the extracted files / game folder.
  - Gloss maps: Wolverine uses two layouts. Most suit parts keep specular colour in RGB and gloss in alpha, which the
    Spider-Man 2 suit shader reads directly. Skin, teeth, claws and fur keep gloss in red and specular in green; those
    are repacked into the suit layout (and re-encoded as BC7) so skin does not come out mirror-glossy.
  Tested with Sabretooth for Peter and Miles: body, gloves, torso, claws and accessories match every skinned bone on
  Miles (Peter: all but the lower-leg twist bones); rendered with the converted textures, everything lines up.

NOT TESTED IN THE GAME
  Checked here (Battle suit, both heroes): the converted models re-import, are skinned to the template skeleton and
  bend correctly; rendered with the converted textures, every part lines up (mask, torso, legs, boots, gloves, Logan's
  arms). The rebuilt materials: the writer reproduces all 29 Spider-Man 2 materials in Downloads\sm2suits byte for byte,
  and every texture a converted material names is in the suit. The textures: headers match real Spider-Man 2 textures,
  and the order of the big mips in the HD part is now checked against real ones (largest first; 2.0 wrote them the
  wrong way round, so its HD textures were scrambled).

HOW TO USE
  1. Start SuitExporter.exe.
  2. Drop one or more folders on the window. Sub-folders are included.
  3. Click a row to check it: suit id, name in game, main model, mask model, menu icon. Change them if the
     guess is wrong. The big box shows the full report for the selected folder.
  4. Tick Peter, Miles or both, choose where to save, and press "Export .suit files".

  Files it understands in a folder:
      name.model   or   name.model.0 + name.model.1          models
      name.material                                           materials
      name.texture + name.hd.texture                          textures (the .hd file is the high-resolution half)
      a Suit Tool project layout: folders 0\ and 1\ with the asset paths inside
  Left out: *.blender.model (Blender import copies), earlier .suit files, empty files, unknown file types.

  Asset paths. Every asset in a .suit needs its game path. The tool finds it, in this order:
      1. from the other files in the folder (a material names its textures, a model names its materials)
      2. from hashes.txt - looked for in the folders above the dropped folder and next to SuitExporter.exe
      3. otherwise the file is placed under suits/<suit id>/...
  The report shows which of the three was used for every file.


WHAT WOULD MAKE A WOLVERINE SUIT PLAYABLE
  The models, materials and textures have to be in Spider-Man 2's own format before they are packed:
      models      rigged to Peter's / Miles's skeleton. The usual way is Blender with the Luna add-on, using
                  characters\hero\hero_spiderman_advanced\hero_spiderman_advanced.model from Spider-Man 2
                  as the template, then exporting in Spider-Man 2 format.
      materials   rebuilt on a material from a Spider-Man 2 suit (Wolverine's shaders do not exist there).
      textures    rewritten in the PC texture layout (the Wolverine ones are in the PS5 layout).
  Export those into a folder, drop that folder here, and the suit packs without the NOT-PLAYABLE mark.
  That mark only means "Wolverine files found". Its absence does not prove a suit works.


WHAT WAS CHECKED
  The .suit writer is a port of Overstrike's Suit Tool. It was compared with that program's own code:
      - the generated configs are byte for byte the same (90 combinations of hero, id and options)
      - Overstrike's .suit reader opens the exported files and every asset comes back unchanged
        (checked on the full hero_wolverine_battle folder: 91 files + 4 configs, for both heroes)
  Not checked: anything inside the game.


OTHER
  Settings (author, save folder, heroes) are kept in SuitExporter-settings.txt next to the exe.
  If something goes wrong at start-up, the message is also written to SuitExporter-error.txt.
  Command line:  SuitExporter.exe --cli <folder>... [--out dir] [--author name] [--heroes peter,miles] [--no-convert]
                 [--blender exe] [--luna dir] [--peter-template file] [--miles-template file]
                 [--sm2-material file] [--sm2-textures dirs] [--wolverine-game dir] [--heads auto|keep|skip]
                 [--hair-donor model] [--hair-colour #rrggbb] [--extracted dir]
                 [--id suit_id] [--names hashes.txt] [--scan]      (output also goes to SuitExporter-cli.txt)

CREDITS AND LICENCE
  The .suit format, the configs and the archive code come from Overstrike and its Suit Tool by Tkachov
  (github.com/Tkachov/Overstrike), GNU General Public License v3. This tool is under the same licence;
  the source is in SuitExporter-source. Build it with build.sh (Mono's mcs, against the .NET Framework
  4.5 reference assemblies). It needs .NET Framework 4.5 or later, which Windows 10 and 11 include.
