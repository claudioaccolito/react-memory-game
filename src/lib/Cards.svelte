<script>
  // @ts-nocheck

  var animals = [
    "🐻",
    "🐴",
    "🐶",
    "🐱",
    "🐷",
    "🦊",
    "🐰",
    "🐵",
    "🐹",
    "🐼",
    "🦁",
    "🦀",
    "🐬",
    "🐢",
    "🦆",
  ];

  function randomFunc() {
    return 0.5 - Math.round(Math.random());
  }

  var animalsPairs = animals.concat(animals).sort(randomFunc);

  var selectedCards = [];
  
  function flipCard(i) {
    if (selectedCards.length === 2) return;

    var cardId = `card-${i}`;
    var selectedCard = document.getElementById(cardId);
    selectedCard.classList.toggle("flipped");
    selectedCards.push(cardId);

    if (selectedCards.length === 2) checkCards();
  }

  function checkCards() {
    var c1 = document.getElementById(selectedCards[0]);
    var c2 = document.getElementById(selectedCards[1]);

    // sono uguali
    if (c1.getAttribute("value") === c2.getAttribute("value")) {
      selectedCards = [];
    } else setTimeout(hideCards, 1500);
  }

  function hideCards() {
    selectedCards.forEach((cardId) => {
      var c = document.getElementById(cardId);
      c.classList.remove("flipped");
    });
    selectedCards = [];
  }
</script>

{#each animalsPairs as animal, i}
  <!-- svelte-ignore a11y-click-events-have-key-events -->
  <span
    value={animal}
    on:click={() => flipCard(i)}
    id={`card-${i}`}
    class="card"
  >
    <!-- card front -->
    <div class="card-front">{animal}</div>

    <!-- card back  -->
    <div class="card-back" />
  </span>
{/each}
