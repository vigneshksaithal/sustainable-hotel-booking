<script>
  import Layout from '../layouts/Layout.astro';

  //
  var user = {
    name: 'John Doe',
    email: '',
    isVegan: false,
    isVegetarian: true,
    
  }

  const hotels = [
    {
      name: 'Hotel Sunny',
      location: 'Paris',
      image:
        'https://images.unsplash.com/photo-1602526270008-8b8b0b0b5b1c?ixid=MnwxMjA3fDB8MHxzZWFyY2h8Mnx8dG9ycmVzJTIwZGVsJTIwcGFpbmUlMjBjaGlsZXxlbnwwfHwwfHw%3D&ixlib=rb-1.2.1&w=1000&q=80',
      description:
        'Ecocamp Patagonia is a luxury tented camp located in Torres del Paine National Park, Chile. The camp is located in the heart of the park, in the Paine Massif, and is surrounded by the Paine River, the Paine Grande and the Paine Chico glaciers.',
      price: 1000,
      sustainablity: {
        // High impact
        usingRenewableEnergy: true,
        rainwaterHarvesting: true,
        foodWasteManagement: true,
        noSingleUsePlastic: true,
        ecoFriedlyCleaningProducts: true,
        carbonOffset: true,
        carbonNeutral: true,
        vegan: true,
        vegetarian: true,
        organic: true,
        localFood: true,
        usesBioGas: false,
        // Medium impact
        usingLED: true,
        paperless: true,
        localSourcing: true,
        usesEndangeredSeaAninmals: false,
        sustainableSourcing: true,
        reuseLaundry: true,
        // Low impact
        usingRecycledPlastic: true,
        usingRecycledPaper: true,
        educateGuests: true,
        occupancyRate: 0.7, // 70% occupancy
        naturalLighting: true,
        onlineBooking: true,
        paperlessCheckIn: true,
        fastCustomerService: true,
        // Innovative solutions
        usesInnovativeSolutions: true,
      },
    },
    {
      name: 'Austin\'s Arts Et Metiers Hotel',
      location: 'Lipa, Batangas, Philippines',
      image:
        'https://www.thefarmatsanbenito.com/wp-content/uploads/2019/10/IMG_20191010_113000-1.jpg',
      description:
        'The Farm at San Benito is a luxury wellness resort in Lipa, Batangas, Philippines. The resort is located in a 500-hectare farm and is surrounded by mountains and rice fields.',
      price: 1000,
      sustainablity: {
        // High impact
        usingRenewableEnergy: true,
        rainwaterHarvesting: true,
        foodWasteManagement: true,
        noSingleUsePlastic: false,
        ecoFriedlyCleaningProducts: true,
        carbonOffset: false,
        carbonNeutral: true,
        vegan: false,
        vegetarian: true,
        organic: true,
        localFood: true,
        usesBioGas: false,
        // Medium impact
        usingLED: true,
        paperless: true,
        localSourcing: true,
        usesEndangeredSeaAninmals: false,
        sustainableSourcing: true,
        reuseLaundry: true,
        // Low impact
        usingRecycledPlastic: true,
        usingRecycledPaper: true,
        educateGuests: true,
        occupancyRate: 0.75, // 70% occupancy
        naturalLighting: true,
        onlineBooking: true,
        paperlessCheckIn: true,
        fastCustomerService: true,
        // Innovative solutions
        usesInnovativeSolutions: true,
      },
    },
    {
      name: 'Appart\'City Confort Paris Grande Bibliothèque',
      location: 'Paris',
      image:
        'https://www.hyaenahouse.com/wp-content/uploads/2019/10/IMG_20191010_113000-1.jpg',
      description:
        'Hyaena House is a luxury wellness resort in Cape Town, South Africa. The resort is located in a 500-hectare farm and is surrounded by mountains and rice fields.',
      price: 1000,
      sustainablity: {
        // High impact
        usingRenewableEnergy: true,
        rainwaterHarvesting: true,
        foodWasteManagement: true,
        noSingleUsePlastic: true,
        ecoFriedlyCleaningProducts: true,
        carbonOffset: false,
        carbonNeutral: false,
        vegan: false,
        vegetarian: true,
        organic: true,
        localFood: true,
        usesBioGas: false,
        // Medium impact
        usingLED: true,
        paperless: true,
        localSourcing: true,
        usesEndangeredSeaAninmals: false,
        sustainableSourcing: true,
        reuseLaundry: true,
        // Low impact
        usingRecycledPlastic: true,
        usingRecycledPaper: true,
        educateGuests: true,
        occupancyRate: 0.8, // 80% occupancy
        naturalLighting: true,
        onlineBooking: true,
        paperlessCheckIn: true,
        fastCustomerService: true,
        // Innovative solutions
        usesInnovativeSolutions: true,
      },
    },
    
  ];

  // Algoithm to calculate the score

  var hotelsList = [];
  function calculateGreenScore(user) {
    let isVegan = user.isVegan;
    let isVegetarian = user.isVegetarian;

    hotels.forEach((hotel) => {
    let sustainabilityScore = 0,
      majorImpactScore = 0,
      mediumImpactScore = 0,
      lowImpactScore = 0;
    let sustainability = hotel.sustainablity;

    // Major Impact (55% of the score)
    if (sustainability.usingRenewableEnergy) mediumImpactScore++;
    if (sustainability.rainwaterHarvesting) majorImpactScore++;
    if (sustainability.foodWasteManagement) majorImpactScore++;
    if (sustainability.noSingleUsePlastic) majorImpactScore++;
    if (sustainability.ecoFriedlyCleaningProducts) majorImpactScore++;
    if (sustainability.carbonOffset) majorImpactScore++;
    if (sustainability.carbonNeutral) majorImpactScore++;
    if (sustainability.localFood) majorImpactScore++;
    if (sustainability.usesBioGas) majorImpactScore++;

    if (user.isVegan) {
      if (sustainability.vegan) majorImpactScore++;
    } else if (user.isVegetarian) {
      if (sustainability.vegetarian) majorImpactScore++;
    }

    if (sustainability.organic) majorImpactScore++;
    sustainabilityScore += majorImpactScore * 0.6;

    // Medium Impact (25% of the score)
    if (sustainability.usingLED) mediumImpactScore++;
    if (sustainability.paperless) mediumImpactScore++;
    if (sustainability.localSourcing) mediumImpactScore++;
    if (sustainability.sustainableSourcing) mediumImpactScore++;

    // If the hotel uses endangered sea animals, it will get a negative score
    // If the hotel is vegitarian or vegan, it will get a positive score
    if (sustainability.vegetarian || sustainability.vegan) {
      mediumImpactScore++;
    } else if (sustainability.usesEndangeredSeaAninmals) {
      mediumImpactScore--;
    }

    // Natural lighting & occupancy rate greatly impacts the score
    if (sustainability.naturalLighting) lowImpactScore = lowImpactScore + 2;
    if (sustainability.occupancyRate > 0.5) lowImpactScore = lowImpactScore + 2;
    sustainabilityScore += mediumImpactScore * 0.25;

    // Minor Impact (15% of the score)
    if (sustainability.usingRecycledPlastic) lowImpactScore++;
    if (sustainability.usingRecycledPaper) lowImpactScore++;
    if (sustainability.educateGuests) lowImpactScore++;
    lowImpactScore = lowImpactScore + sustainability.occupancyRate * 0.15;
    if (sustainability.onlineBooking) lowImpactScore++;
    if (sustainability.paperlessCheckIn) lowImpactScore++;
    if (sustainability.fastCustomerService) lowImpactScore++;
    sustainabilityScore += lowImpactScore * 0.15;

    // Innovative solutions (5% of the score)
    if (sustainability.usesInnovativeSolutions)
      sustainabilityScore = sustainabilityScore + 0.05;

    // Roundoff the score
    sustainabilityScore = Math.round(sustainabilityScore);

    if (sustainabilityScore > 0) {
      hotelsList.push({
        name: hotel.name,
        location: hotel.location,
        image: hotel.image,
        description: hotel.description,
        price: hotel.price,
        sustainablityScore: sustainabilityScore,
      });
    }
  });
  }

  $: {
    calculateGreenScore(user.isVegan);
  }
</script>

  <main>
    <h1 class="text-2xl text-center font-semibold text-slate-700 mb-12">Sustainable Hotel Booking</h1>

    <!-- Checkbox -->
    <div class="flex gap-4 pb-4 px-2">
      <div>
        <input type="checkbox" bind:checked={user.isVegetarian} />
        <label for="Vegetarian"> Vegetarian</label>
      </div>
      <div>
        <input type="checkbox" bind:checked={user.isVegan} />
        <label for="Vegan"> Vegan</label>
      </div>
      <div>
        <input type="checkbox" />
        <label for="Budget freindly">Budget freindly</label>
      </div>
      <div>
        <input type="checkbox" />
        <label for="Local food">Local food</label>
      </div>
    </div>
    <div class="grid grid-cols-1 gap-2">
      {#each hotelsList as hotel}
        <div
          class="bg-white p-5 rounded-2xl border-2 border-slate-200 shadow-sm"
        >
          <div class="grid grid-cols-12 justify-between">
            <h1 class="col-span-10 text-xl font-semibold">{hotel.name}</h1>
            <span
              class="col-span-2 bg-green-600 text-center py-2 px-2 rounded-full text-sm font-semibold text-white"
            >
              {hotel.sustainablityScore}/10
            </span>
          </div>
          <p class="text-sm">{hotel.location}</p>
        </div>
      {/each}
    </div>
  </main>
