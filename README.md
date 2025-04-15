"use client";
import React, { useState } from "react"; // ✅ Fixed: added useState

function MainComponent() {
  const [step, setStep] = useState(1); // 🆗 Step controller

  const [character, setCharacter] = useState({
    name: "",
    seeming: "",
    kith: "",
    legacies: {
      seelie: "",
      unseelie: "",
    },
    attributes: {
      physical: { strength: 1, dexterity: 1, stamina: 1 },
      social: { charisma: 1, manipulation: 1, composure: 1 },
      mental: { intelligence: 1, wits: 1, resolve: 1 },
    },
    attributePoints: {
      primary: "primary",
      secondary: "secondary",
      tertiary: "tertiary",
    },
    skills: {
      physical: {},
      social: {},
      mental: {},
    },
    skillPoints: {
      primary: 11,
      secondary: 7,
      tertiary: 4,
    },
    arts: {}, // will be filled by user
    artPoints: 3,
    realms: {},
    realmPoints: 4,
    backgroundsAndMerits: {
      backgrounds: {},
      merits: {},
    },
    backgroundAndMeritPoints: 10,
    flaws: {},
    flawPoints: 2,
    concept: "",
    court: "",
  });

  const seemings = ["Foundling", "Errant", "Wilder", "Eidolon", "Legend"];

  const kiths = [
    "Boggan",
    "Clurichaun",
    "Eshu",
    "Nocker",
    "Pooka",
    "Redcap",
    "Sluagh",
    "Troll",
  ];
  const kithDetails = {
    Boggan: {
      theme: "Hospitality, community, humble power",
      birthrights: [
        "Craftwork – When unobserved by anyone except fellow Boggans, you complete physical tasks in one-third the time. In chronological terms, reduce crafting time for practical or artistic projects by 2 intervals (e.g., days become hours).",
        "Hands of Insight – Gain a +2 bonus dice pool to Crafts or Larceny rolls involving physical work (e.g., repairs, cooking, tailoring) when focused and uninterrupted."
      ],
      frailty:
        "Compelled to Aid – When witnessing genuine need, roll Willpower (Difficulty 3); failure compels immediate assistance, possibly against better judgment."
    },
    Clurichaun: {
      theme: "Fortune, contracts, social dazzle",
      birthrights: [
        "Twinkling of an Eye – When Calling the Wyrd (rousing Glamour), gain +2 dice on Leadership, Performance, and Empathy rolls.",
        "Gift of Gab – May reroll one failed die on Persuasion or Subterfuge rolls when negotiating or storytelling."
      ],
      frailty:
        "Bound by Truth – Clurichaun cannot lie. Doing so breaks all current social contracts and prevents forming new ones for a year and a day."
    },
    Eshu: {
      theme: "Destiny, charisma, the road",
      birthrights: [
        "Spirit Pathways – Eshu always arrive when the story is best served.",
        "Fate-Touched Socialite – Add +1 die to any social pool when in a new setting or among strangers."
      ],
      frailty:
        "Adventure's Draw – Must make a Willpower roll (Difficulty 3) to resist narrative challenges or riddles."
    },
    Nocker: {
      theme: "Creation as criticism, flawed genius",
      birthrights: [
        "Fix-It – Gain +1 die to any roll involving engineering, invention, or repair.",
        "Flaw Spotting – Make a free Wits + Technology (or Investigation) test once per scene to find weaknesses in constructs."
      ],
      frailty:
        "Cursed Craft – Anything a Nocker builds has a cosmetic or minor functional flaw that cannot be removed."
    },
    Pooka: {
      theme: "Chaos, instinct, animal dream-forms",
      birthrights: [
        "Animal Form – May shift into one animal form when alone (cost: 1 Glamour).",
        "Confidante – +1 die to Persuasion or Subterfuge when joking or emotionally engaging others."
      ],
      frailty:
        "Liar's Tongue – Must roll Willpower (Diff 3) to speak plainly. Otherwise, must twist facts."
    },
    Redcap: {
      theme: "Appetite, menace, unstoppable force",
      birthrights: [
        "Dark Appetite – May consume anything and bypass a barrier once per scene by doing so.",
        "Bully Browbeat – Gain +2 dice to Intimidation when threatening violence or consumption."
      ],
      frailty:
        "Insatiable Hunger – Must consume something unnatural or taboo each session or suffer −1 to Social rolls."
    },
    Sluagh: {
      theme: "Secrets, liminality, the unspeakable",
      birthrights: [
        "Sharpened Senses – +2 dice to detect the hidden or subtle. May speak to the dead under calm conditions.",
        "Squirm – Can fit through any space the size of their head. Escape attempts gain +2 dice."
      ],
      frailty:
        "Curse of Silence – Can only speak in whispers. −2 dice to vocal Social rolls unless listener strains or is enchanted."
    },
    Troll: {
      theme: "Strength, honor, tragedy of trust",
      birthrights: [
        "Titanic Strength – While defending others or upholding oaths, gain Potence equal to half your Glamour (rounded down) for one scene.",
        "Unyielding – +2 dice to resist Compulsion, Dominate, or coercion when defending others or oaths."
      ],
      frailty:
        "Honor-Bound – If an oath is broken, lose all Birthrights and Fae powers until redemption. May suffer spiritual 'Staining'."
    }
  };
  const legacyTypes = {
    seelie: [
      "Beast (Protector)",
      "Outlaw (Freedom Fighter)",
      "Romantic (Dreamer)",
      "Sage (Mentor)",
      "Warrior (Honorable)",
      "Trickster (Teacher)"
    ],
    unseelie: [
      "Beast (Dominator)",
      "Outlaw (Rebel)",
      "Romantic (Manipulator)",
      "Sage (Hoarder)",
      "Warrior (Ruthless)",
      "Trickster (Deceiver)"
    ]
  };

  const legacyDetails = {
    Beast: {
      theme: "Instinct, Strength, and Territory",
      seelie: "Protects the weak, follows nature's balance, defends kin",
      unseelie: "Dominates the weak, asserts dominance through fear or violence",
      outlook: "Distrustful of politics, follows personal code or pack loyalty",
      compulsion: "Must immediately defend or assert dominance when threatened or insulted"
    },
    Outlaw: {
      theme: "Rebellion, Defiance, and Lawbreaking",
      seelie: "Fights injustice, rebels to defend freedom or dreamers",
      unseelie: "Breaks rules for gain, joy, or personal vengeance",
      outlook: "At odds with Court structures, often revered by youth and radicals"
    },
    Romantic: {
      theme: "Passion, Love, and Longing",
      seelie: "Idealist, pursues true love and beauty for its own sake",
      unseelie: "Uses love as manipulation; sees affection as power",
      outlook: "Often tragic or obsessive; thrives in Courts of beauty, art, or decadence",
      compulsion: "Must act to gain the affection of someone, or express a grand romantic gesture"
    },
    Sage: {
      theme: "Knowledge, Wisdom, and Secrets",
      seelie: "Uplifts others with knowledge; acts as mentor and advisor",
      unseelie: "Hoards wisdom; manipulates through secrets and half-truths",
      outlook: "Often advisors, record-keepers, or occultists within Freeholds",
      compulsion: "Must either share or hide critical knowledge at great cost"
    },
    Warrior: {
      theme: "Battle, Resolve, and Code",
      seelie: "Fights with honor; defends the weak and just cause",
      unseelie: "Fights to win, no matter the means or collateral damage",
      outlook: "Often tied to oathkeeping and Court enforcement",
      compulsion: "Must never back down from a challenge or insult"
    },
    Trickster: {
      theme: "Change, Laughter, and Chaos",
      seelie: "Uses wit to expose flaws in authority and to teach through humor",
      unseelie: "Lies and misleads for self-gain or amusement",
      outlook: "Feared and revered in equal parts; often keeps Freeholds humble",
      compulsion: "Must deceive or mock"
    }
  };
  const courts = [
    "Seelie (Order)",
    "Unseelie (Passion)",
    "Shadow Court (Secrecy)"
  ];

  const seemingDetails = {
    Foundling: {
      title: "The Untamed Dreamers",
      stage: "Newly escaped from Arcadia (under 5 years)",
      theme: "Raw Glamour, untamed and surreal",
      physical: "Shimmering forms, glowing eyes, shifting hair; dreamstuff clings to them",
      effects: "Environmental oddities—lights flicker, animals stare, rain curves unnaturally",
      mortalPerception: "Seen as imaginary friends or fairy tales by kids; unnerving to adults",
      mechanicalBenefit: [
        "+1 die to Glamour-fueled spells or Contracts involving Nature or Scene Realms",
        "Gains Glamour passively when witnessed by innocents (e.g., children or dreamers)",
        "+15 bonus xp"
      ],
      drawback: "Attracts supernatural attention; −1 die to Stealth or disguise in highly Banal areas"
    },
    Errant: {
      title: "The Liminal Wanderers",
      stage: "Becoming accustomed to the Waking world (6+ years)",
      theme: "Graceful dream logic, magnetism, and allure",
      physical: "Perfected features, voice lingers, clothing made of impossible materials",
      effects: "Tech glitches nearby; they fade into backgrounds unnaturally",
      mortalPerception: "Fascinating, dreamy, socially magnetic",
      mechanicalBenefit: [
        "+2 dice to Manipulation or Persuasion with groups",
        "−2 dice to tech-based surveillance targeting them",
        "+35 bonus xp"
      ],
      drawback: "Must make Willpower check to resist mysterious distractions"
    },
    Wilder: {
      title: "The Rebels of the Dreaming",
      stage: "Mid-evolution changelings—conflicted, powerful, chaotic (10+ years)",
      theme: "Raw energy, unpredictability, danger",
      physical: "Sketch-like outlines, independent shadows, reflections that lag",
      effects: "Lights dim, environments subtly distort",
      mortalPerception: "Charismatic but unnerving; distrusted by authority",
      mechanicalBenefit: [
        "+1 die to Initiative and Wits rolls in tense or urban areas",
        "Once/session may 'glitch' reality—reroll a failed social or stealth test",
        "+55 bonus xp"
      ],
      drawback: "Must roll Resolve + Composure in stress; failure triggers instinctual behavior"
    },
    Eidolon: {
      title: "The Architects of Fate",
      stage: "Advanced changelings—defined identities, stabilizing forces (16+ years)",
      theme: "Mastery of fae identity and mortal anchoring",
      physical: "Gravity of presence, temperature shifts around them",
      effects: "Time feels slower, memories linger near them",
      mortalPerception: "Seen as leaders or legends-in-the-making",
      mechanicalBenefit: [
        "+2 dice on Presence rolls when invoking authority or myth",
        "−1 Glamour cost when casting in bonded locations (e.g., homes)",
        "+75 bonus xp"
      ],
      drawback: "Draws Dreamers and predators; may be targeted by Arcadian forces"
    },
    Legend: {
      title: "Living Myths",
      stage: "Transcendence; near archetypal beings (25+ years)",
      theme: "Power so vast it warps the world around them",
      physical: "Eyes like landscapes, echoing voices, shadows of past selves",
      effects: "Doors open, fate bends, weather responds",
      mortalPerception: "Inspires awe; even skeptics believe again",
      mechanicalBenefit: [
        "Once/session may declare an Oath/Prophecy as truth (costs Glamour/Willpower)",
        "+1 difficulty for opponents resisting their magic or persuasion",
        "+95 bonus xp"
      ],
      drawback: "Risk of Ephemeral Fractures that alert Dauntain or destabilize Glamour pools"
    }
  };
  const attributeCategories = {
    physical: {
      name: "Physical",
      description:
        "These govern raw strength, agility, and endurance—key traits for changelings navigating both mundane and chimerical threats.",
      attributes: {
        strength: {
          name: "Strength",
          description: "The measure of raw muscle power and ability to exert force.",
          levels: {
            1: "Feeble – Struggles with basic physical tasks.",
            2: "Average – Can move furniture and break wood with effort.",
            3: "Above Average – Athlete-level strength.",
            4: "Powerful – Can lift extremely heavy objects.",
            5: "Superhuman – Can shatter obstacles with ease."
          }
        },
        dexterity: {
          name: "Dexterity",
          description: "Agility, speed, and coordination; important for combat and precision.",
          levels: {
            1: "Clumsy – Fumbles basic coordination.",
            2: "Average – Competent motor skills.",
            3: "Skilled – Like a dancer or martial artist.",
            4: "Exceptional – Acrobat-level fluidity.",
            5: "Otherworldly – Unreal precision and speed."
          }
        },
        stamina: {
          name: "Stamina",
          description: "Endurance and toughness—how well you can resist hardship.",
          levels: {
            1: "Fragile – Tires easily, very vulnerable.",
            2: "Average – Can keep up with physical activity.",
            3: "Hardy – Great endurance, can take hits.",
            4: "Indomitable – Rarely tires, shrugs off pain.",
            5: "Unyielding – Survives nearly anything."
          }
        }
      }
    },

    social: {
      name: "Social",
      description:
        "These govern influence, presence, and interpersonal skill—vital for fae interaction and manipulation.",
      attributes: {
        charisma: {
          name: "Charisma",
          description: "Ability to attract and inspire through personality.",
          levels: {
            1: "Uninspiring – Easily ignored.",
            2: "Likable – Casual and friendly.",
            3: "Captivating – Others follow you naturally.",
            4: "Mesmerizing – Commands rooms with presence.",
            5: "Mythic – Legendary charm and magnetism."
          }
        },
        manipulation: {
          name: "Manipulation",
          description: "Cunning and subtlety in conversation and control.",
          levels: {
            1: "Transparent – Terrible liar.",
            2: "Persuasive – Can bluff and negotiate.",
            3: "Deceptive – Skilled manipulator.",
            4: "Masterful – Orchestrates entire situations.",
            5: "Legendary – Can rewrite reality with words."
          }
        },
        composure: {
          name: "Composure",
          description: "Self-control and grace under social and magical pressure.",
          levels: {
            1: "Shaky – Emotionally reactive.",
            2: "Collected – Usually calm.",
            3: "Steady – Rarely rattled.",
            4: "Unshakable – Immune to panic.",
            5: "Unbreakable – Iron-clad mental discipline."
          }
        }
      }
    },

    mental: {
      name: "Mental",
      description:
        "Cognitive capabilities—intelligence, reaction speed, and strength of mind.",
      attributes: {
        intelligence: {
          name: "Intelligence",
          description: "Reasoning, education, and memory.",
          levels: {
            1: "Simple – Struggles with complexity.",
            2: "Competent – Understands common subjects.",
            3: "Sharp – Learns fast and solves problems.",
            4: "Genius – Expert in complex ideas.",
            5: "Visionary – Sees patterns beyond reality."
          }
        },
        wits: {
          name: "Wits",
          description: "Reaction speed and awareness in dynamic situations.",
          levels: {
            1: "Slow – Lags behind.",
            2: "Alert – Can keep up.",
            3: "Quick – Snappy decision-maker.",
            4: "Instinctive – Near precognition.",
            5: "Preternatural – Uncannily responsive."
          }
        },
        resolve: {
          name: "Resolve",
          description: "Determination and focus—resisting mental intrusion or distraction.",
          levels: {
            1: "Unfocused – Quick to give up.",
            2: "Determined – Can stay on task with effort.",
            3: "Strong-willed – Highly goal-oriented.",
            4: "Indomitable – Refuses to quit.",
            5: "Unyielding – Resists even magical influence."
          }
        }
      }
    }
  };
  const skillCategories = {
    physical: {
      name: "Physical Skills",
      description: "Skills based on strength, agility, and physical resilience.",
      skills: {
        athletics: {
          name: "Athletics",
          description: "Running, climbing, swimming, and feats of general physical prowess."
        },
        brawl: {
          name: "Brawl",
          description: "Unarmed combat, from bar fights to martial arts."
        },
        craft: {
          name: "Craft",
          description: "Building, repairing, and working with your hands—artisan or tradeskill."
        },
        drive: {
          name: "Drive",
          description: "Piloting cars and other ground vehicles under normal or extreme conditions."
        },
        firearms: {
          name: "Firearms",
          description: "Use of guns, crossbows, and other projectile weapons."
        },
        larceny: {
          name: "Larceny",
          description: "Lockpicking, pickpocketing, and general criminal trickery."
        },
        melee: {
          name: "Melee",
          description: "Skill in using hand-to-hand weapons: swords, axes, staves, etc."
        },
        stealth: {
          name: "Stealth",
          description: "Moving silently, hiding, and avoiding detection."
        },
        survival: {
          name: "Survival",
          description: "Wilderness knowledge: tracking, foraging, shelter-building."
        }
      }
    },

    social: {
      name: "Social Skills",
      description: "Skills involving charm, manipulation, and interpersonal savvy.",
      skills: {
        animalKen: {
          name: "Animal Ken",
          description: "Understanding and calming animals; building trust with beasts."
        },
        etiquette: {
          name: "Etiquette",
          description: "Navigating social rules, customs, and rituals gracefully."
        },
        insight: {
          name: "Insight",
          description: "Reading emotions, intentions, and underlying truth from people."
        },
        intimidation: {
          name: "Intimidation",
          description: "Using fear, menace, or pressure to get what you want."
        },
        leadership: {
          name: "Leadership",
          description: "Inspiring, commanding, and organizing others to act."
        },
        performance: {
          name: "Performance",
          description: "Acting, singing, dancing—any expressive art that holds an audience."
        },
        persuasion: {
          name: "Persuasion",
          description: "Getting others to agree, cooperate, or see your view."
        },
        streetwise: {
          name: "Streetwise",
          description: "Knowing how to get things done in urban or underground environments."
        },
        subterfuge: {
          name: "Subterfuge",
          description: "Lying, bluffing, and deception to mislead others."
        }
      }
    },

    mental: {
      name: "Mental Skills",
      description: "Skills related to intellect, perception, and knowledge.",
      skills: {
        academics: {
          name: "Academics",
          description: "Formal education: history, law, literature, and similar fields."
        },
        awareness: {
          name: "Awareness",
          description: "General perception—sensing danger, spotting ambushes, feeling shifts in energy."
        },
        finance: {
          name: "Finance",
          description: "Managing money, investments, and economic systems."
        },
        investigation: {
          name: "Investigation",
          description: "Gathering clues, following leads, solving mysteries."
        },
        medicine: {
          name: "Medicine",
          description: "Diagnosing and treating wounds, illness, or trauma."
        },
        occult: {
          name: "Occult",
          description: "Knowledge of magic, myth, supernatural beings, and forgotten lore."
        },
        politics: {
          name: "Politics",
          description: "Understanding power structures and how to leverage them."
        },
        science: {
          name: "Science",
          description: "Knowledge of biology, chemistry, physics, and more."
        },
        technology: {
          name: "Technology",
          description: "Using and understanding digital tools, gadgets, and systems."
        }
      }
    }
  };
  const arts = {
    chicanery: {
      name: "Chicanery",
      description: "The Art of illusion, trickery, and misdirection."
    },
    metamorphosis: {
      name: "Metamorphosis",
      description: "The ability to alter form—yours or another’s."
    },
    naming: {
      name: "Naming",
      description: "True name magic. Control through knowledge of essence."
    },
    primal: {
      name: "Primal",
      description: "Command over the elements and natural forces."
    },
    sovereign: {
      name: "Sovereign",
      description: "Authority, commands, and social control among the fae."
    },
    wayfare: {
      name: "Wayfare",
      description: "Movement, speed, teleportation, and spatial bending."
    }
  };

  const realms = {
    actor: {
      name: "Actor",
      description: "Affects mortals—humans and those unawakened to fae nature."
    },
    fae: {
      name: "Fae",
      description: "Targets changelings, fae creatures, and enchanted beings."
    },
    nature: {
      name: "Nature",
      description: "Affects animals, plants, and natural forces."
    },
    prop: {
      name: "Prop",
      description: "Manipulates physical objects and items."
    },
    scene: {
      name: "Scene",
      description: "Casts over entire areas, rooms, or environments."
    },
    time: {
      name: "Time",
      description: "Influences timing, speed, or temporal sequence."
    },
    gremayre: {
      name: "Gremayre",
      description: "Interacts with Glamour, magical theory, and arcane structure."
    }
  };
  const backgrounds = {
    allies: {
      name: "Allies",
      description: "Mortal friends who will help you in times of need.",
      maxDots: 5
    },
    contacts: {
      name: "Contacts",
      description: "Useful individuals who provide information and gossip.",
      maxDots: 5
    },
    holdings: {
      name: "Holdings",
      description: "Property or territory under your control.",
      maxDots: 5
    },
    resources: {
      name: "Resources",
      description: "Your wealth, income, and material assets.",
      maxDots: 5
    },
    retinue: {
      name: "Retinue",
      description: "Servants, followers, or a personal entourage.",
      maxDots: 5
    },
    title: {
      name: "Title",
      description: "Your standing within Kithain society or Court politics.",
      maxDots: 5
    },
    treasures: {
      name: "Treasures",
      description: "Magic items or relics you possess.",
      maxDots: 5
    }
  };

  const merits = {
    acute_sense: {
      name: "Acute Sense",
      description: "One of your senses is exceptionally sharp.",
      cost: 1
    },
    ambidextrous: {
      name: "Ambidextrous",
      description: "You can use both hands with equal skill.",
      cost: 1
    },
    common_sense: {
      name: "Common Sense",
      description: "You instinctively know what choices avoid trouble.",
      cost: 1
    },
    danger_sense: {
      name: "Danger Sense",
      description: "You feel when something dangerous is nearby.",
      cost: 2
    },
    eidetic_memory: {
      name: "Eidetic Memory",
      description: "You remember everything you see or hear.",
      cost: 2
    },
    iron_will: {
      name: "Iron Will",
      description: "You are highly resistant to mental influence.",
      cost: 3
    }
  };
  const flaws = {
    bedlamProne: {
      name: "Bedlam Prone",
      description: "Susceptible to Glamour overload and madness.",
      cost: 2,
      mechanics: "Roll Willpower (Diff 7) when exposed to high Glamour or intense dreams.",
      example: "Hallucinates fae creatures during emotional stress."
    },
    chimericalDeformity: {
      name: "Chimerical Deformity",
      description: "A visible flaw in your fae mien.",
      cost: 3,
      mechanics: "−2 dice to Social rolls in fae society.",
      example: "Twisted limbs, glowing scars, or constantly shifting features."
    },
    bannedTransformation: {
      name: "Banned Transformation",
      description: "You are unable to use certain transformative powers.",
      cost: 3,
      mechanics: "May not activate certain Arts (like Metamorphosis).",
      example: "A pooka who cannot shift into animal form."
    },
    geas: {
      name: "Geas",
      description: "Magically bound to obey a mystical rule.",
      cost: 2,
      mechanics: "Must follow a specific restriction or suffer consequences.",
      example: "Cannot cross running water. Must speak truth on moonlit nights."
    },
    otherworldly: {
      name: "Otherworldly",
      description: "You behave or appear unnervingly fae in mortal society.",
      cost: 2,
      mechanics: "−2 to Social rolls with mortals.",
      example: "Speaks in rhyme, has shimmering skin, or eerie posture."
    },
    infamous: {
      name: "Infamous",
      description: "Your reputation precedes you, and not in a good way.",
      cost: [2, 3],
      mechanics: "Suffers penalties in social interactions with fae.",
      example: "Oathbreaker, kith traitor, or accused Dream-thief."
    },
    debtBound: {
      name: "Debt-Bound",
      description: "Owe significant favors to a powerful fae or entity.",
      cost: [2, 3],
      mechanics: "Must perform services or favors regularly or face Glamour penalties.",
      example: "Owed magic to a Court noble or bound to a Freehold spirit."
    },
    dreamingSick: {
      name: "Dreaming-Sick",
      description: "You suffer physically when exposed to Glamour.",
      cost: 3,
      mechanics: "Take minor damage or penalties after casting Arts or touching free Glamour.",
      example: "Nausea, splitting migraines, nosebleeds."
    },
    huntedRenegade: {
      name: "Hunted Renegade",
      description: "You are actively pursued by enemies.",
      cost: [3, 4],
      mechanics: "Storyteller regularly introduces encounters with your pursuers.",
      example: "Targeted by the Wild Hunt, Dauntain, or mortal technocrats."
    },
    faeAmnesia: {
      name: "Fae Amnesia",
      description: "You have forgotten key elements of your fae self.",
      cost: 2,
      mechanics: "Do not know your true Kith, Oaths, or Glamour origins.",
      example: "Forgets old motley, missing childhood memories."
    }
  };
  const handleNext = () => {
    setStep((prev) => Math.min(prev + 1, 11)); // 11 is final step
  };

  const handleBack = () => {
    setStep((prev) => Math.max(prev - 1, 1)); // 1 is first step
  };

  const renderStep = () => {
    switch (step) {
      case 1:
        return <Step1Seeming character={character} setCharacter={setCharacter} />;
      case 2:
        return <Step2Kith character={character} setCharacter={setCharacter} />;
      case 3:
        return <Step3Legacy character={character} setCharacter={setCharacter} />;
      case 4:
        return <Step4Attributes character={character} setCharacter={setCharacter} />;
      case 5:
        return <Step5Skills character={character} setCharacter={setCharacter} />;
      case 6:
        return <Step6Arts character={character} setCharacter={setCharacter} />;
      case 7:
        return <Step7Realms character={character} setCharacter={setCharacter} />;
      case 8:
        return <Step8Backgrounds character={character} setCharacter={setCharacter} />;
      case 9:
        return <Step9Flaws character={character} setCharacter={setCharacter} />;
      case 10:
        return <Step10Concept character={character} setCharacter={setCharacter} />;
      case 11:
        return <Step11Court character={character} setCharacter={setCharacter} />;
      default:
        return <div className="text-red-500">Invalid step selected.</div>;
    }
  };
  return (
    <div className="min-h-screen bg-white dark:bg-gray-900 p-4 md:p-8">
      <div className="max-w-4xl mx-auto">
        <header className="mb-8">
          <h1 className="text-4xl md:text-6xl font-bold text-gray-900 dark:text-white">
            Changeling Character Generator
          </h1>
          <p className="text-gray-700 dark:text-gray-300 mt-2">
            Step {step} of 11
          </p>
        </header>

        <section className="mb-8">
          <div className="flex justify-between items-center">
            <button
              onClick={handleBack}
              disabled={step === 1}
              className="px-6 py-3 border border-gray-300 dark:border-gray-700 text-gray-900 dark:text-white rounded-md hover:bg-gray-100 dark:hover:bg-gray-800 transition disabled:opacity-50"
            >
              Back
            </button>
            <button
              onClick={handleNext}
              disabled={step === 11}
              className="px-6 py-3 bg-gray-900 dark:bg-gray-700 text-white rounded-md hover:bg-gray-700 dark:hover:bg-gray-600 transition disabled:opacity-50"
            >
              Next
            </button>
          </div>
        </section>

        <main className="bg-white dark:bg-gray-800 p-6 rounded-lg border border-gray-200 dark:border-gray-700">
          {renderStep()}
        </main>
      </div>
    </div>
  );
}
// steps/Step1Seeming.js
import React from "react";

function Step1Seeming({ character, setCharacter }) {
  const seemings = ["Foundling", "Errant", "Wilder", "Eidolon", "Legend"];

  const handleChange = (e) => {
    setCharacter((prev) => ({
      ...prev,
      seeming: e.target.value
    }));
  };

  return (
    <div className="space-y-4">
      <h2 className="text-2xl font-bold text-gray-900 dark:text-white">Seeming Selection</h2>
      <p className="text-gray-700 dark:text-gray-300">
        Choose how long your changeling has walked the world.
      </p>
      <select
        value={character?.seeming || ""}
        onChange={handleChange}
        className="w-full p-3 border border-gray-300 dark:border-gray-700 rounded-lg bg-white dark:bg-gray-800 text-gray-900 dark:text-white"
      >
        <option value="">Select Seeming</option>
        {seemings.map((s) => (
          <option key={s} value={s}>
            {s}
          </option>
        ))}
      </select>
    </div>
  );
}

export default Step1Seeming;
// steps/Step2Kith.js
import React from "react";

function Step2Kith({ character, setCharacter }) {
  const kiths = [
    "Boggan",
    "Clurichaun",
    "Eshu",
    "Nocker",
    "Pooka",
    "Redcap",
    "Sluagh",
    "Troll"
  ];

  const handleChange = (e) => {
    setCharacter((prev) => ({
      ...prev,
      kith: e.target.value
    }));
  };

  return (
    <div className="space-y-4">
      <h2 className="text-2xl font-bold text-gray-900 dark:text-white">Kith Selection</h2>
      <p className="text-gray-700 dark:text-gray-300">
        Choose your fae lineage.
      </p>
      <select
        value={character?.kith || ""}
        onChange={handleChange}
        className="w-full p-3 border border-gray-300 dark:border-gray-700 rounded-lg bg-white dark:bg-gray-800 text-gray-900 dark:text-white"
      >
        <option value="">Select Kith</option>
        {kiths.map((kith) => (
          <option key={kith} value={kith}>
            {kith}
          </option>
        ))}
      </select>
    </div>
  );
}

export default Step2Kith;
// steps/Step2Kith.js
import React from "react";

function Step2Kith({ character, setCharacter }) {
  const kiths = [
    "Boggan",
    "Clurichaun",
    "Eshu",
    "Nocker",
    "Pooka",
    "Redcap",
    "Sluagh",
    "Troll"
  ];

  const handleChange = (e) => {
    setCharacter((prev) => ({
      ...prev,
      kith: e.target.value
    }));
  };

  return (
    <div className="space-y-4">
      <h2 className="text-2xl font-bold text-gray-900 dark:text-white">Kith Selection</h2>
      <p className="text-gray-700 dark:text-gray-300">
        Choose your fae lineage.
      </p>
      <select
        value={character?.kith || ""}
        onChange={handleChange}
        className="w-full p-3 border border-gray-300 dark:border-gray-700 rounded-lg bg-white dark:bg-gray-800 text-gray-900 dark:text-white"
      >
        <option value="">Select Kith</option>
        {kiths.map((kith) => (
          <option key={kith} value={kith}>
            {kith}
          </option>
        ))}
      </select>
    </div>
  );
}

export default Step2Kith;
// steps/Step3Legacy.js
import React from "react";

function Step3Legacy({ character, setCharacter }) {
  const legacyTypes = {
    seelie: [
      "Beast (Protector)",
      "Outlaw (Freedom Fighter)",
      "Romantic (Dreamer)",
      "Sage (Mentor)",
      "Warrior (Honorable)",
      "Trickster (Teacher)"
    ],
    unseelie: [
      "Beast (Dominator)",
      "Outlaw (Rebel)",
      "Romantic (Manipulator)",
      "Sage (Hoarder)",
      "Warrior (Ruthless)",
      "Trickster (Deceiver)"
    ]
  };

  const handleLegacyChange = (type, value) => {
    setCharacter((prev) => ({
      ...prev,
      legacies: {
        ...prev.legacies,
        [type]: value
      }
    }));
  };

  return (
    <div className="space-y-6">
      <h2 className="text-2xl font-bold text-gray-900 dark:text-white">Legacy Selection</h2>
      <p className="text-gray-700 dark:text-gray-300">
        Choose your Seelie and Unseelie natures.
      </p>

      <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
        <div className="space-y-2">
          <label className="block text-gray-700 dark:text-gray-300">Seelie Legacy</label>
          <select
            value={character?.legacies?.seelie || ""}
            onChange={(e) => handleLegacyChange("seelie", e.target.value)}
            className="w-full p-3 border border-gray-300 dark:border-gray-700 rounded-lg bg-white dark:bg-gray-800 text-gray-900 dark:text-white"
          >
            <option value="">Select Seelie Legacy</option>
            {legacyTypes.seelie.map((legacy) => (
              <option key={legacy} value={legacy}>
                {legacy}
              </option>
            ))}
          </select>
        </div>

        <div className="space-y-2">
          <label className="block text-gray-700 dark:text-gray-300">Unseelie Legacy</label>
          <select
            value={character?.legacies?.unseelie || ""}
            onChange={(e) => handleLegacyChange("unseelie", e.target.value)}
            className="w-full p-3 border border-gray-300 dark:border-gray-700 rounded-lg bg-white dark:bg-gray-800 text-gray-900 dark:text-white"
          >
            <option value="">Select Unseelie Legacy</option>
            {legacyTypes.unseelie.map((legacy) => (
              <option key={legacy} value={legacy}>
                {legacy}
              </option>
            ))}
          </select>
        </div>
      </div>
    </div>
  );
}

export default Step3Legacy;
// steps/Step4Attributes.js
import React from "react";

function Step4Attributes({ character, setCharacter }) {
  const categories = ["physical", "social", "mental"];
  const attributes = {
    physical: ["strength", "dexterity", "stamina"],
    social: ["charisma", "manipulation", "composure"],
    mental: ["intelligence", "wits", "resolve"]
  };

  const pointValues = {
    primary: 10,
    secondary: 7,
    tertiary: 4
  };

  const handleAttributeChange = (category, attr, value) => {
    const newValue = Math.max(1, Math.min(5, value));
    setCharacter((prev) => ({
      ...prev,
      attributes: {
        ...prev.attributes,
        [category]: {
          ...prev.attributes[category],
          [attr]: newValue
        }
      }
    }));
  };

  const handlePriorityChange = (category, priority) => {
    setCharacter((prev) => ({
      ...prev,
      attributePoints: {
        ...prev.attributePoints,
        [category]: priority
      }
    }));
  };

  const getTotalDots = () =>
    Object.values(character.attributes).reduce(
      (total, group) => total + Object.values(group).reduce((sum, val) => sum + val, 0),
      0
    );

  return (
    <div className="space-y-6">
      <h2 className="text-2xl font-bold text-gray-900 dark:text-white">Attributes</h2>

      <p className="text-gray-700 dark:text-gray-300">Distribute attribute dots. Total used: {getTotalDots()}/20</p>

      <div className="grid grid-cols-1 md:grid-cols-3 gap-4">
        {categories.map((category) => (
          <div key={category}>
            <label className="block text-sm font-medium text-gray-700 dark:text-gray-300 mb-1">
              {category.charAt(0).toUpperCase() + category.slice(1)}
            </label>
            <select
              value={character.attributePoints[category]}
              onChange={(e) => handlePriorityChange(category, e.target.value)}
              className="w-full p-2 border border-gray-300 dark:border-gray-700 rounded bg-white dark:bg-gray-800 text-gray-900 dark:text-white"
            >
              <option value="primary">Primary (10)</option>
              <option value="secondary">Secondary (7)</option>
              <option value="tertiary">Tertiary (4)</option>
            </select>
          </div>
        ))}
      </div>

      {categories.map((category) => (
        <div key={category} className="bg-gray-50 dark:bg-gray-700 p-4 rounded-lg mt-4">
          <h3 className="text-lg font-semibold text-gray-900 dark:text-white capitalize">{category}</h3>
          {attributes[category].map((attr) => (
            <div key={attr} className="flex items-center justify-between py-2">
              <span className="text-gray-700 dark:text-gray-300 capitalize">{attr}</span>
              <div className="flex space-x-1">
                {[1, 2, 3, 4, 5].map((dot) => (
                  <button
                    key={dot}
                    onClick={() => handleAttributeChange(category, attr, dot)}
                    className={`w-5 h-5 rounded-full border ${
                      character.attributes[category][attr] >= dot
                        ? "bg-gray-900 dark:bg-gray-200"
                        : "bg-white dark:bg-gray-600"
                    } border-gray-300 dark:border-gray-400`}
                  />
                ))}
              </div>
            </div>
          ))}
        </div>
      ))}
    </div>
  );
}

export default Step4Attributes;
// steps/Step5Skills.js
import React from "react";

function Step5Skills({ character, setCharacter }) {
  const skillCategories = {
    physical: ["athletics", "brawl", "craft", "drive", "firearms", "larceny", "melee", "stealth", "survival"],
    social: ["animalKen", "etiquette", "insight", "intimidation", "leadership", "performance", "persuasion", "streetwise", "subterfuge"],
    mental: ["academics", "awareness", "finance", "investigation", "medicine", "occult", "politics", "science", "technology"]
  };

  const handleSkillChange = (category, skill, value) => {
    const newValue = Math.max(0, Math.min(5, value));
    setCharacter((prev) => ({
      ...prev,
      skills: {
        ...prev.skills,
        [category]: {
          ...prev.skills[category],
          [skill]: newValue
        }
      }
    }));
  };

  const getTotalSkillDots = () => {
    return Object.values(character.skills).reduce((total, group) => {
      return total + Object.values(group).reduce((sum, val) => sum + (val || 0), 0);
    }, 0);
  };

  return (
    <div className="space-y-6">
      <h2 className="text-2xl font-bold text-gray-900 dark:text-white">Skills</h2>
      <p className="text-gray-700 dark:text-gray-300">Distribute your skill dots. Total used: {getTotalSkillDots()}/22</p>

      {Object.entries(skillCategories).map(([category, skills]) => (
        <div key={category} className="bg-gray-50 dark:bg-gray-700 p-4 rounded-lg">
          <h3 className="text-lg font-semibold text-gray-900 dark:text-white capitalize">{category}</h3>
          {skills.map((skill) => (
            <div key={skill} className="flex items-center justify-between py-2">
              <span className="text-gray-700 dark:text-gray-300 capitalize">{skill}</span>
              <div className="flex space-x-1">
                {[0, 1, 2, 3, 4, 5].map((dot) => (
                  <button
                    key={dot}
                    onClick={() => handleSkillChange(category, skill, dot)}
                    className={`w-5 h-5 rounded-full border ${
                      (character.skills[category]?.[skill] || 0) >= dot
                        ? "bg-gray-900 dark:bg-gray-200"
                        : "bg-white dark:bg-gray-600"
                    } border-gray-300 dark:border-gray-400`}
                  />
                ))}
              </div>
            </div>
          ))}
        </div>
      ))}
    </div>
  );
}

export default Step5Skills;
// steps/Step6Arts.js
import React from "react";

function Step6Arts({ character, setCharacter }) {
  const arts = {
    chicanery: "Illusion and deception.",
    metamorphosis: "Shapechanging and transformation.",
    naming: "True name power and essence manipulation.",
    primal: "Elemental control.",
    sovereign: "Command and authority over others.",
    wayfare: "Movement, speed, and teleportation."
  };

  const handleArtChange = (artKey, value) => {
    const newValue = Math.max(0, Math.min(5, value));
    const current = character.arts[artKey] || 0;
    const used = Object.values(character.arts).reduce((sum, v) => sum + (v || 0), 0);
    const total = 3;

    if (used - current + newValue > total) {
      return;
    }

    setCharacter((prev) => ({
      ...prev,
      arts: {
        ...prev.arts,
        [artKey]: newValue
      }
    }));
  };

  const totalUsed = Object.values(character.arts).reduce((sum, v) => sum + (v || 0), 0);

  return (
    <div className="space-y-6">
      <h2 className="text-2xl font-bold text-gray-900 dark:text-white">Arts</h2>
      <p className="text-gray-700 dark:text-gray-300">Assign up to 3 total dots in Arts. Used: {totalUsed}/3</p>

      {Object.entries(arts).map(([key, desc]) => (
        <div key={key} className="border-b border-gray-300 dark:border-gray-600 py-4">
          <div className="flex justify-between items-center mb-1">
            <span className="text-gray-900 dark:text-white capitalize font-medium">{key}</span>
            <div className="flex space-x-1">
              {[0, 1, 2, 3, 4, 5].map((dot) => (
                <button
                  key={dot}
                  onClick={() => handleArtChange(key, dot)}
                  className={`w-5 h-5 rounded-full border ${
                    (character.arts[key] || 0) >= dot
                      ? dot === 0
                        ? "bg-gray-300 dark:bg-gray-600"
                        : "bg-gray-900 dark:bg-gray-200"
                      : "bg-white dark:bg-gray-600"
                  } border-gray-300 dark:border-gray-500`}
                />
              ))}
            </div>
          </div>
          <p className="text-sm text-gray-600 dark:text-gray-400">{desc}</p>
        </div>
      ))}
    </div>
  );
}

export default Step6Arts;
// steps/Step7Realms.js
import React from "react";

function Step7Realms({ character, setCharacter }) {
  const realms = {
    actor: "Mortals – affects non-supernatural humans.",
    fae: "Changelings – affects other fae beings.",
    nature: "Animals and plants – affects natural life.",
    prop: "Inanimate objects and items.",
    scene: "A location, such as a room or field.",
    time: "Temporal perception and manipulation.",
    gremayre: "Interaction with magical constructs or Glamour."
  };

  const handleRealmChange = (realmKey, value) => {
    const newValue = Math.max(0, Math.min(5, value));
    const current = character.realms[realmKey] || 0;
    const used = Object.values(character.realms).reduce((sum, v) => sum + (v || 0), 0);
    const total = 4;

    if (used - current + newValue > total) return;

    setCharacter((prev) => ({
      ...prev,
      realms: {
        ...prev.realms,
        [realmKey]: newValue
      }
    }));
  };

  const totalUsed = Object.values(character.realms).reduce((sum, v) => sum + (v || 0), 0);

  return (
    <div className="space-y-6">
      <h2 className="text-2xl font-bold text-gray-900 dark:text-white">Realms</h2>
      <p className="text-gray-700 dark:text-gray-300">
        Assign up to 4 total dots in Realms. Used: {totalUsed}/4
      </p>

      {Object.entries(realms).map(([key, desc]) => (
        <div key={key} className="border-b border-gray-300 dark:border-gray-600 py-4">
          <div className="flex justify-between items-center mb-1">
            <span className="text-gray-900 dark:text-white capitalize font-medium">{key}</span>
            <div className="flex space-x-1">
              {[0, 1, 2, 3, 4, 5].map((dot) => (
                <button
                  key={dot}
                  onClick={() => handleRealmChange(key, dot)}
                  className={`w-5 h-5 rounded-full border ${
                    (character.realms[key] || 0) >= dot
                      ? dot === 0
                        ? "bg-gray-300 dark:bg-gray-600"
                        : "bg-gray-900 dark:bg-gray-200"
                      : "bg-white dark:bg-gray-600"
                  } border-gray-300 dark:border-gray-500`}
                />
              ))}
            </div>
          </div>
          <p className="text-sm text-gray-600 dark:text-gray-400">{desc}</p>
        </div>
      ))}
    </div>
  );
}

export default Step7Realms;
// steps/Step8Backgrounds.js
import React from "react";

function Step8Backgrounds({ character, setCharacter }) {
  const backgroundOptions = {
    allies: "Mortal friends who will assist you.",
    contacts: "Sources of information and rumors.",
    holdings: "Lands, Freeholds, or properties you control.",
    resources: "Money, goods, and wealth.",
    retinue: "Loyal attendants or servants.",
    title: "Social rank or position within fae society.",
    treasures: "Magical items or relics in your possession."
  };

  const totalCap = character.backgroundAndMeritPoints || 10;

  const getTotalUsed = () =>
    Object.values(character.backgroundsAndMerits.backgrounds).reduce((sum, val) => sum + (val || 0), 0) +
    Object.values(character.backgroundsAndMerits.merits).reduce((sum, val) => sum + (val || 0), 0);

  const handleBackgroundChange = (key, value) => {
    const newValue = Math.max(0, Math.min(5, value));
    const current = character.backgroundsAndMerits.backgrounds[key] || 0;
    const used = getTotalUsed();

    if (used - current + newValue > totalCap) return;

    setCharacter((prev) => ({
      ...prev,
      backgroundsAndMerits: {
        ...prev.backgroundsAndMerits,
        backgrounds: {
          ...prev.backgroundsAndMerits.backgrounds,
          [key]: newValue
        }
      }
    }));
  };

  return (
    <div className="space-y-6">
      <h2 className="text-2xl font-bold text-gray-900 dark:text-white">Backgrounds</h2>
      <p className="text-gray-700 dark:text-gray-300">
        Assign dots in backgrounds. Total used (including merits): {getTotalUsed()}/{totalCap}
      </p>

      {Object.entries(backgroundOptions).map(([key, desc]) => (
        <div key={key} className="border-b border-gray-300 dark:border-gray-600 py-4">
          <div className="flex justify-between items-center mb-1">
            <span className="text-gray-900 dark:text-white capitalize font-medium">{key}</span>
            <div className="flex space-x-1">
              {[0, 1, 2, 3, 4, 5].map((dot) => (
                <button
                  key={dot}
                  onClick={() => handleBackgroundChange(key, dot)}
                  className={`w-5 h-5 rounded-full border ${
                    (character.backgroundsAndMerits.backgrounds[key] || 0) >= dot
                      ? "bg-gray-900 dark:bg-gray-200"
                      : "bg-white dark:bg-gray-600"
                  } border-gray-300 dark:border-gray-500`}
                />
              ))}
            </div>
          </div>
          <p className="text-sm text-gray-600 dark:text-gray-400">{desc}</p>
        </div>
      ))}
    </div>
  );
}

export default Step8Backgrounds;
// steps/Step9Flaws.js
import React from "react";

function Step9Flaws({ character, setCharacter }) {
  const flawOptions = {
    bedlamProne: {
      name: "Bedlam Prone",
      cost: 2,
      description: "Prone to Glamour overload and madness."
    },
    chimericalDeformity: {
      name: "Chimerical Deformity",
      cost: 3,
      description: "Visible flaw in your fae mien."
    },
    faeAmnesia: {
      name: "Fae Amnesia",
      cost: 2,
      description: "You’ve forgotten vital parts of your fae identity."
    },
    infamous: {
      name: "Infamous",
      cost: [2, 3],
      description: "You are widely mistrusted or reviled in fae society."
    },
    debtBound: {
      name: "Debt-Bound",
      cost: [2, 3],
      description: "You owe favors or service to a powerful being."
    },
    dreamingSick: {
      name: "Dreaming-Sick",
      cost: 3,
      description: "Glamour exposure causes physical illness."
    },
    huntedRenegade: {
      name: "Hunted Renegade",
      cost: [3, 4],
      description: "You are actively pursued by enemies."
    }
  };

  const selectedFlaws = Object.keys(character.flaws || {});
  const selectedCount = selectedFlaws.length;

  const updateFlaw = (key, value) => {
    setCharacter((prev) => {
      const updated = { ...prev.flaws };

      if (value === 0) {
        delete updated[key];
      } else {
        const cost = Array.isArray(flawOptions[key].cost)
          ? flawOptions[key].cost[value - 1]
          : flawOptions[key].cost;

        updated[key] = cost;
      }

      return { ...prev, flaws: updated };
    });
  };

  return (
    <div className="space-y-6">
      <h2 className="text-2xl font-bold text-gray-900 dark:text-white">Flaws</h2>
      <p className="text-gray-700 dark:text-gray-300">
        Choose exactly 2 flaws. Selected: {selectedCount}/2
      </p>

      <div className="grid grid-cols-1 md:grid-cols-2 gap-6">
        {Object.entries(flawOptions).map(([key, flaw]) => (
          <div key={key} className="border border-gray-300 dark:border-gray-700 p-4 rounded-lg">
            <h3 className="font-semibold text-gray-900 dark:text-white">{flaw.name}</h3>
            <p className="text-sm text-gray-600 dark:text-gray-400 mb-2">{flaw.description}</p>

            {Array.isArray(flaw.cost) ? (
              <select
                value={character.flaws[key] || 0}
                onChange={(e) => updateFlaw(key, parseInt(e.target.value))}
                disabled={selectedCount >= 2 && !character.flaws[key]}
                className="w-full p-2 border border-gray-300 dark:border-gray-600 rounded bg-white dark:bg-gray-700 text-gray-900 dark:text-white"
              >
                <option value={0}>None</option>
                {flaw.cost.map((c, i) => (
                  <option key={c} value={i + 1}>
                    Level {i + 1} ({c} pts)
                  </option>
                ))}
              </select>
            ) : (
              <button
                onClick={() =>
                  updateFlaw(key, character.flaws[key] ? 0 : 1)
                }
                disabled={selectedCount >= 2 && !character.flaws[key]}
                className={`px-3 py-1 mt-2 rounded ${
                  character.flaws[key]
                    ? "bg-red-700 text-white"
                    : "bg-gray-200 dark:bg-gray-600 dark:text-white"
                } ${selectedCount >= 2 && !character.flaws[key] ? "opacity-50 cursor-not-allowed" : ""}`}
              >
                {character.flaws[key] ? "Remove" : "Select"}
              </button>
            )}
          </div>
        ))}
      </div>

      {selectedCount !== 2 && (
        <div className="mt-4 p-3 bg-yellow-100 dark:bg-yellow-900 text-yellow-800 dark:text-yellow-200 rounded">
          Please select exactly two flaws to continue.
        </div>
      )}
    </div>
  );
}

export default Step9Flaws;
// steps/Step10Concept.js
import React from "react";

function Step10Concept({ character, setCharacter }) {
  const handleChange = (e) => {
    setCharacter((prev) => ({
      ...prev,
      concept: e.target.value
    }));
  };

  return (
    <div className="space-y-6">
      <h2 className="text-2xl font-bold text-gray-900 dark:text-white">Character Concept</h2>
      <p className="text-gray-700 dark:text-gray-300">
        Write a brief summary of your changeling's personality, origin, or story arc.
      </p>
      <textarea
        value={character.concept}
        onChange={handleChange}
        rows={6}
        className="w-full p-4 border border-gray-300 dark:border-gray-700 rounded-lg bg-white dark:bg-gray-800 text-gray-900 dark:text-white"
        placeholder="E.g. A Wilder Pooka exiled from Arcadia, trying to rebuild lost memories among the streets of New Seattle..."
      />
    </div>
  );
}

export default Step10Concept;
// steps/Step11Court.js
import React from "react";

function Step11Court({ character, setCharacter }) {
  const courts = [
    "Seelie (Order)",
    "Unseelie (Passion)",
    "Shadow Court (Secrecy)"
  ];

  const handleChange = (e) => {
    setCharacter((prev) => ({
      ...prev,
      court: e.target.value
    }));
  };

  return (
    <div className="space-y-6">
      <h2 className="text-2xl font-bold text-gray-900 dark:text-white">Court Affiliation</h2>
      <p className="text-gray-700 dark:text-gray-300">
        Choose your political or philosophical allegiance within fae society.
      </p>
      <select
        value={character.court}
        onChange={handleChange}
        className="w-full p-3 border border-gray-300 dark:border-gray-700 rounded-lg bg-white dark:bg-gray-800 text-gray-900 dark:text-white"
      >
        <option value="">Select a Court</option>
        {courts.map((court) => (
          <option key={court} value={court}>
            {court}
          </option>
        ))}
      </select>
    </div>
  );
}

export default Step11Court;



export default MainComponent;
