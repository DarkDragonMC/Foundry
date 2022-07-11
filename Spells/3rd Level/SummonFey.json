/*
Original Code taken from Kuffeh1's Summon Beast Spell Macro:
https://github.com/Kuffeh1/Foundry/blob/main/Spells/Level%202/Summon%20Beast

Modified by DarkDragonMC for Summon Fey Spell Macro. 

Modules Used - MidiQOL, ItemMacro, Warpgate, JB2A (Free or Patreon), Sequencer [for the effects, optional]

Set Up - You need to ensure you have an actor called 'Fey Spirit'

MidiQOL OnUse -  ItemMacro - before active effect
*/

const casterToken = game.actors.get(args[0].actor._id);
const tokenD = canvas.tokens.get(args[0].tokenId);
const spelllevel = args[0].spellLevel;
const level = casterToken.data.data.details.level;

let choices = await warpgate.dialog([

    {
        type:'header', 
        label:`Type`
    },
    {
        type: 'radio', 
        label: `Fuming`, 
    },
    {
        type: 'radio', 
        label: `Mirthful`, 
    },
    {
        type: 'radio', 
        label: `Tricksy`, 
    },
    ],
    "⚔️ Choose your spirit:",
    "Call Forth!")

let spiritArray = [choices[1],choices[2],choices[3]];  
spiritArray = spiritArray.filter(Boolean);
let summon = spiritArray[0];

const summonType = `Fey Spirit`;

let baseHP = '';
        
        if (summon === 'Fuming')
            { baseHP = 30; }
        if (summon === 'Mirthful')
            { baseHP = 30; }
        if (summon === 'Tricksy')  
            { baseHP = 30; }  
        
let upcastHP = ' ';
        if (spelllevel >= 3)
            { upcastHP = `${((spelllevel-3)*10)}`; }
        
let spiritHP = ' ';
         if (spelllevel < 3)
                {spiritHP = parseInt(baseHP)}  
         if (spelllevel >= 3)
                { spiritHP =  parseInt(baseHP) + parseInt(upcastHP); } 

let spiritImg = '';
        
        if (summon === 'Fuming')
            { spiritImg = 'https://assets.forge-vtt.com/60d61d34d28f090bc36517c0/Images/tokens/NPCs/Summons/Fey%20Spirit/fey_spirit.Token.webp'; }
        if (summon === 'Mirthful')
            { spiritImg = 'https://assets.forge-vtt.com/60d61d34d28f090bc36517c0/Images/tokens/NPCs/Summons/Fey%20Spirit/fey_spirit.Token.webp'; }
        if (summon === 'Tricksy')  
            { spiritImg = 'https://assets.forge-vtt.com/60d61d34d28f090bc36517c0/Images/tokens/NPCs/Summons/Fey%20Spirit/fey_spirit.Token.webp'; }    
            
let spiritMove = '';

        if (summon === 'Fuming')
            { spiritMove = {walk: 40}; }
        if (summon === 'Mirthful')
            { spiritMove = {walk: 40}; }
        if (summon === 'Tricksy')  
            { spiritMove = {walk: 40}; }              

let spiritAC = '';

        if (summon === 'Fuming')
            { spiritAC = 12 + spelllevel; }
        if (summon === 'Mirthful')
            { spiritAC = {walk: 40}; }
        if (summon === 'Tricksy')  
            { spiritAC = {walk: 40}; }   

let updates = 
    {
    token: {
      'img': spiritImg ,
            },
    actor: {
      'name':`${summon} of ${casterToken.name}`,
      'data.attributes.ac.formula' : 12 + spelllevel,
      'data.attributes.hp' : {value: spiritHP, max: spiritHP},
      'data.details.cr' : level ,
      'data.attributes.movement' : spiritMove,
            },  
    embedded: {  
      Item: {
        "Multiattack":{
          'name': `Multiattack (${Math.floor(spelllevel/2)} attacks)`},
        "Shortsword":{
          'data.damage.parts': [[`1d6  + @mod + ${spelllevel}`, 'piercing']]},
            }
              },
    }

    async function myEffectFunction(template) {

let effect = ' ';
            if (summon === 'Fuming')
                { effect = 'modules/JB2A_DnD5e/Library/Generic/Impact/PartSideImpactSmoke02_01_Regular_Blue_600x600.webm'; }
            if (summon === 'Mirthful')
                { effect = 'modules/JB2A_DnD5e/Library/Generic/Impact/GroundCrackImpact_01_Regular_Orange_600x600.webm'; } 
            if (summon === 'Tricksy')
                { effect = 'modules/JB2A_DnD5e/Library/Generic/Liquid/LiquidSplash01_Regular_Blue_400x400.webm'; }
 
//prep summoning area
        new Sequence()
            .effect()
                .file(effect)
                .atLocation(template)
                .center()
                .scale(0.3)
                //.belowTokens()
            .play()
        }
        
        async function postEffects(template, token) {
        //bring in our token
        new Sequence()
            .animation()
                .on(token)
                    .fadeIn(1500)
            .play()
        }
        
        const callbacks = {
            pre: async (template,update) => {
                myEffectFunction(template);
                await warpgate.wait(500);
            },
            post: async (template, token) => {
            postEffects(template,token);
            await warpgate.wait(500);
            }
        };
  
  const options = {controllingActor: actor};

  await warpgate.spawn(summonType, updates, callbacks, options);