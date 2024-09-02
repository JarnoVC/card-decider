<template>
  <div class="app-container">
    <Randomizer @randomize="randomizeSideMenu" />

    <main>
      <MainCardList :cards="visibleCards" @card-selected="handleCardSelected" @flip-card="flipCard" />
      <SideMenu :selectedCard="selectedCard" />
    </main>
  </div>
</template>

<script>
import MainCardList from './components/MainCardList.vue';
import SideMenu from './components/SideMenu.vue';
import Randomizer from './components/RandomizerFunction.vue';

export default {
  components: { MainCardList, SideMenu, Randomizer },
  data() {
    return {
      cards: [
        { id: 1, name: 'Disappearing act', type:'Debuff' ,effect: "Forces one of the user's allies to phase out of existence momentarily, making them intangible and immune to physical attacks, but also preventing them from dealing damage. This could mean that Solana loses an ally for the duration of the fight", imageUrl: require('@/assets/Disappearing act_cutout.png'), flipped: false },
        { id: 2, name: 'Spiral of time', type:'Debuff' ,effect: "The user's mind is send forwards in time, causing temporary amnesia. This makes the user forget key combat skills and tactics. Solana can no longer use her spells for a brief period", imageUrl: require('@/assets/Spiral of time_cutout.png'), flipped: false },
        { id: 3, name: 'Starless night', type:'Debuff' ,effect: "Summons shadowy apparitions that hinder the user's visibility, making it impossible to avoid the enemy's next attack", imageUrl: require('@/assets/Starless night_cutout.png'), flipped: false },
        { id: 4, name: 'The betrayer', type:'Debuff' ,effect: 'Creates illusory voices that sow doubts and confusion, making it impossoble for the user to coordinate with their allies for a short time', imageUrl: require('@/assets/The betrayer_cutout.png'), flipped: false },
        { id: 5, name: 'The butterfly', type:'Debuff' ,effect: "Causes small, seemingly insignificant actions to have disproportionately chaotic consequences, leading to unintended and unpredictable outcomes", imageUrl: require('@/assets/The butterfly_cutout.png'), flipped: false },
        { id: 6, name: 'The collapse', type:'Debuff' ,effect: "Reality starts folding in on itself, causing the user's attacks and movement to exist in multiple states simultaneously, making it difficult to predict their actions. This could mean that when Solana attacks it could simultaneously be happening from different angles towards the enemy and at different lengths from the target", imageUrl: require('@/assets/The collapse_cutout.png'), flipped: false },
        { id: 7, name: 'The echo', type:'Buff' ,effect: 'For your next three attacks, a second attack roll can be performed to cause a ghostly apparition to repeat that attack on the same target. Repeat attacks inherit all traits of the original attack', imageUrl: require('@/assets/The echo_cutout.png'), flipped: false },
        { id: 8, name: 'The fates', type:'Buff' ,effect: 'Upon landing three attacks on an enemy, that enemy will take a disproportionate amount of damage compared to the three attacks. Lower level enemies may die instantly. Switching targets will reset the count', imageUrl: require('@/assets/The fates_cutout.png'), flipped: false },
        { id: 9, name: 'The hanged man', type:'Buff' ,effect: "Grants a critical insight on Solana's current combat and survival situation. The more dire the circumstances, the more information she aquires", imageUrl: require('@/assets/The hanged man_cutout.png'), flipped: false },
        { id: 10, name: 'The incubus', type:'Debuff', effect: "The telltale effect of an Incubus's presence starts filling the air, wisps of pheromones clouding everyone's judgement. This could result in a surprising sexual end to a conflict", imageUrl: require('@/assets/The incubus_cutout.png'), flipped: false },
        { id: 11, name: 'The leviathan', type:'Buff' ,effect: "Calls upon the might of the leviathan, turning the user's arms into whip-like tentacles, especially effective near lakes or oceans as the user can take control of the water", imageUrl: require('@/assets/The Leviathan2_cutout.png'), flipped: false },
        { id: 12, name: 'The shapeshifter', type:'Debuff' ,effect: "Transforms the user's weapon into an enchanted scepter that randomly alters its form, making attacks less predictable and controllable.", imageUrl: require('@/assets/The shapeshifter_cutout.png'), flipped: false },
        { id: 13, name: 'The thief', type:'Buff' ,effect: "Pick a random magical effect in the area and bend it to your will; Magic and spells cannot be altered from their original form (i.e you can't turn a fireball into a handheld torch), and passive effects that linger will be converted for a set amount of time depending on the effect and the source of the effect", imageUrl: require('@/assets/The thief_cutout.png'), flipped: false },
        { id: 14, name: 'The thorned rose', type:'Debuff' ,effect: "Summons magical vines covered in thorns that bury themselves in the user's skin, restraining their movement and agility", imageUrl: require('@/assets/The thorned rose_cutout.png'), flipped: false },
        { id: 15, name: 'The twin', type:'Debuff' ,effect: "Creates a malevolent doppelgänger that mirrors the user's actions, but with reversed effects, making their every move unpredictable. (The doppelgänger's actions don't directly mirror the user's intentions. For instance, if the user swings their sword, the doppelgänger might perform a similar motion, but instead of dealing damage, it could inadvertently heal an opponent or trigger a magical effect)", imageUrl: require('@/assets/The twin_cutout.png'), flipped: false },
        { id: 16, name: 'The valkyrie', type:'Buff' ,effect: 'Summons spectral wings that allows the user to fly, granting the user increased mobility and evasion for a brief period of time', imageUrl: require('@/assets/The valkyrie_cutout.png'), flipped: false },
        { id: 17, name: 'Northern winds',type:'Buff' ,effect: "Temporarily imbues the user's weapon with icy power, freezing enemies on cotact and slowing their movement", imageUrl: require('@/assets/Northern winds_cutout.png'), flipped: false },
        { id: 18, name: 'The chronomancer',type:'Buff' ,effect: 'Manipulates time, allowing the user to peer briefly into the future and doge attacks with increased agility for a short duration', imageUrl: require('@/assets/The chronomancer_cutout.png'), flipped: false },
        { id: 19, name: 'The devil', type: 'Debuff' ,effect: 'For the duration of the fight, Solana is restricted to a certain area around the strongest enemy in the fight. This is a physical law and cannot be bend; she will be pulled into the requisite radius if she starts outside that radius. Attempting to leave that area will be like pressing against a brick wall', imageUrl: require('@/assets/The devil_cutout.png'), flipped: false },
        { id: 20, name: 'The divergent',type:'Debuff' ,effect: "Solana experiences the sensations of her from an alternate reality where she is defeated in combat and kept as a trophy of sexual conquest. This includes enemies Solana has previously fought and enemies that she is yet to face", imageUrl: require('@/assets/The divergent_cutout.png'), flipped: false },
        { id: 21, name: 'The empyrean', type:'Neutral' ,effect: "Solana can empower herself or any target with a burst of divine power. For three turns, the target deals additional damage with their physical attacks that is increased based on the type of enemy they land on. Power is increased further the darker the field of battle is. If the target is unable to vanquish their intended enemy withing that time period, they lose the divine empowerment and are instead blinded for three turns. The divine empowerment and the blindness cannot be purged by any meansn even by other card effects", imageUrl: require('@/assets/The empyrean_cutout.png'), flipped: false },
        { id: 22, name: 'The forest nymph',type:'Buff' ,effect: "Summons a magical forest spirit to fight alongside the suer, providing additional support in battle. Works in the same way as Solana's bone widow when attacking or can offer to heal the party", imageUrl: require('@/assets/The forest nymph_cutout.png'), flipped: false },
        { id: 23, name: 'The fountain', type: 'Neutral' ,effect: "Mana surges the field, allowing for infinite spellcasts. For three turns, anything and everyone can cast magic without cost. The surge will dissipate after that time, after which a feedback effect will prevent use of magic for three turns. Magic effects that linger after cast will remain even after the feedback period begins. Any magic that requires continuous channeling is cancelled at the start of the feedback period", imageUrl: require('@/assets/The fountain_cutout.png'), flipped: false },
        { id: 24, name: 'The gavel', type: 'Neutral' ,effect: "The eart shakes violently beneath your feet periodically, throwing everyone involved off-balance with each pulse. Certain terrain may be exempt from this effect, while other terrain may be severly affected in contrast. Airborne enemies are not affected.", imageUrl: require('@/assets/The gavel_cutout.png'), flipped: false },
        { id: 25, name: 'The honorbound', type: 'Neutral',effect: "All spell-limits are removed from Solana and she is healed to full. She must engaga in one-on-one combat with a random enemy on the field, which will also be fully healed. No other entity can interfere in this duel. The effect of the card does not dispell until one of the participants is unable to fight, after which all effects of this card are brought to and end", imageUrl: require('@/assets/The honorbound_cutout.png'), flipped: false },
        { id: 26, name: 'The still', type: 'Neutral' ,effect: "Any and all mana-driven effects active on the field are forcibly surpressed, regardless of source. Any effect that resulted from magic will remain (i.e a fire started by a flame spell will remain, but the flame spell itself will be extinguished and surpressed)", imageUrl: require('@/assets/The still_cutout.png'), flipped: false },
        { id: 27, name: 'The lovers', type:'Neutral' ,effect: "The line between friend and foe becomes heavily blurred - all combatants on the field lose sense of who is their enemy. Enemies will prioritize each other in combat, with the exception of higher-sentience enemies of higher rank, which may be able to break the effect. Solana may break this effect for her allies as well, for which the chances of success depend on her current physical and magical states as well as a roll. If the effect is not broken, Solana and her allies become hostile to one another", imageUrl: require('@/assets/The lovers_cutout.png'), flipped: false },
        { id: 28, name: 'The loving mother', type: 'Buff' ,effect: 'Conjures a protective arcane energy shield around the user, reducing or negating incoming damage for a limited time', imageUrl: require('@/assets/The loving mother_cutout.png'), flipped: false },
        { id: 29, name: 'The lurking shadow', type:'Buff' ,effect: 'Allows the user to meld with the shadows, becoming nearly invisible to enemies for a short duration, granting steath and surprise advantage', imageUrl: require('@/assets/The lurking shadow_cutout.png'), flipped: false },
        { id: 30, name: 'The mirror', type:'Buff' ,effect: 'Reflects a portion of incoming damage back to the attacker, turning the tables on those who dare to harm the user', imageUrl: require('@/assets/The mirror_cutout.png'), flipped: false },
        { id: 31, name: 'The reaper', type: 'Buff' ,effect: "Your next attack is like death itself - it cannot be blocked, avoided, or nullified in any way. Strength and lethality of the attack is unchanged (i.e throwing a pebble at an anemey isn't going to suddenly kill them outright)", imageUrl: require('@/assets/The reaper_cutout.png'), flipped: false },
        { id: 32, name: 'The shadow', type: 'Debuff' ,effect: "Solana's shadow develops a tear between dimensions. she has a set amount of time to end the conflict she's in. Failure to defeat her enemies or resolve the conflict she's in at the time will result in her shadow being fully torn, after which she will be pulled into it and teleported to the Shadow Plane (one of the Planewalker's Mantle routes). Allies and enemies are not pulled in with her", imageUrl: require('@/assets/The shadow_cutout.png'), flipped: false },
        { id: 33, name: 'The siren', type:'Buff' ,effect: "Enchants the user's voice, captivating enemies and momentarily distracting them, reducing their combat effectiveness and forcing their focus on Solana", imageUrl: require('@/assets/The siren_cutout.png'), flipped: false },
        { id: 34, name: 'The imp',type:'Buff' ,effect: 'Envelops the user in etheral flames, enhancing their attacks with fire and causing enemies to burn over time', imageUrl: require('@/assets/The imp_cutout.png'), flipped: false },
        { id: 35, name: 'The storm', type: 'Neutral' ,effect: "The battlefield becomes electrified. Bolts of lightning can strike from the sky, the ground, or walls/ceiling of any location, regardless of whether the material of those constructs are conductive or not. Metal objects can attract lightning surges", imageUrl: require('@/assets/The storm_cutout.png'), flipped: false },
        { id: 36, name: 'The whisper', type: 'Debuff' ,effect: "All of Solana's outgoing attacks are cut to a fraction of their strength, even if she attempts to exert herself for more force. Effects can last for five turns", imageUrl: require('@/assets/The whisper_cutout.png'), flipped: false },
        { id: 37, name: 'The weft', type: 'Debuff' ,effect: 'Reality itself folds in on Solana, and in three turns she will be bound and helpless for three turns. These binds cannot be severed or broken by any means. Her bindings do not interfere with any external force (i.e an attack to the wrists do not do any less damage if wrists are bound)', imageUrl: require('@/assets/The weft_cutout.png'), flipped: false },
        { id: 38, name: 'The two of swords', type:'Neutral' ,effect: "Pain sustained by all individuals that are actively engaged in combat is shared among all combatants regardless of alliance. Dead combatants are not included in this effect. Injuries are not transfered but the pain of the injuries may temporarily force the recipients to mimic its effects. For example, receiving pain from someone whose leg is severed may cause a severe limp in the person with both legs intact. The person missing a leg will gain a mana projection that allows them to limp to the same degree", imageUrl: require('@/assets/The two of swords_cutout.png'), flipped: false },
        { id: 39, name: 'The tarrasque', type: 'Neutral' ,effect: "Solana becomes impossibly resistant to any and all forms of damage, and develops twice as much strength as her baseline. She also regenerates up to half her vitality and will, which is roll-dependent. During this time, her mobility and ability to attack are severly hampered. She is also unable to use magic during this time. This effect can be turned off at will after three turns have elapsed", imageUrl: require('@/assets/The tarrasque_cutout.png'), flipped: false },
        { id: 40, name: 'The stygian', type:'Neutral' ,effect: "The card assesses Solana and her companions in the midst of battle. Those that are closer to death are empowered and will deal significantly more damage with any attack. Even a glancing blow may inflict grievous wounds. Those that are closer to full strength will be weakened and will lose vitality. If the loss of vitality reduces them to half their vitality, the former empowerment effect will be granted and the weaken will be removed", imageUrl: require('@/assets/The stygian_cutout.png'), flipped: false },
        // Add the rest of your 40 cards here
      ],       hiddenCard: { id: 41, name: 'The jester', type: 'Secret', effect: 'Solana is can select a card of her choosing' ,imageUrl: require('@/assets/The jester_cutout.png'), flipped: false },
      selectedCard: null
    };
  },
  computed: {
    visibleCards() {
      return this.cards.filter(card => card.id !== 41); // Exclude the hidden card
    },
  },
  methods: {
    randomizeSideMenu() {
      const randomNumber = Math.floor(Math.random() * 50) + 1;
      if (randomNumber === 1) {
        this.selectedCard = this.hiddenCard; // 1 in 100 chance to select hidden card
      } else {
        this.selectedCard = this.cards[Math.floor(Math.random() * this.cards.length)];
      }
    },
    flipCard(id) {
      this.cards = this.cards.map(card =>
        card.id === id ? { ...card, flipped: !card.flipped } : card
      );
    }
  }
};
</script>
<style scoped>
.app-container {
  border: 10px solid #c19a6b;
  background-color: #f5f5dc;
  padding: 20px;
  display: flex;
  flex-direction: column;
  min-height: 100vh;
  box-sizing: border-box;
  overflow: visible; /* Allow overflow in case of enlarged elements */
  position: relative;
}

main {
  display: flex;
  flex: 1;
  overflow: visible; /* Ensure the content in main can overflow without clipping */
  position: relative;
}


.card-display {
  flex: 3;
  position: relative; /* Ensure that cards within the grid can overflow */
  z-index: 1; /* Default z-index */
}

.random-result {
  flex: 1;
  padding: 20px;
  background-color: #e3c99f;
  border-left: 2px solid #c19a6b;
}
</style>
