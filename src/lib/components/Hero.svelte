<script lang="ts">
  import { onMount } from 'svelte';
  import { navigate } from 'svelte-routing';

  let searchLocation = '';
  let searchStartDate = '';
  let searchEndDate = '';
  
  function handleSearch(e: Event) {
    e.preventDefault();
    
    // Build query parameters
    const queryParams = new URLSearchParams();
    if (searchLocation) queryParams.set('location', searchLocation);
    if (searchStartDate) queryParams.set('start', searchStartDate);
    if (searchEndDate) queryParams.set('end', searchEndDate);
    
    // Navigate to search page with query parameters
    navigate(`/search?${queryParams.toString()}`);
  }
  
  // Set default dates
  onMount(() => {
    const tomorrow = new Date();
    tomorrow.setDate(tomorrow.getDate() + 1);
    
    const nextWeek = new Date();
    nextWeek.setDate(nextWeek.getDate() + 7);
    
    searchStartDate = tomorrow.toISOString().slice(0, 10);
    searchEndDate = nextWeek.toISOString().slice(0, 10);
  });
</script>

<section class="relative h-[calc(100vh-0px)] min-h-[600px] bg-neutral-900 overflow-hidden">
  <div class="absolute inset-0 z-0">
    <div class="absolute inset-0 bg-gradient-to-r from-black/80 to-black/40"></div>
    <img 
      src="https://images.pexels.com/photos/17609550/pexels-photo-17609550/free-photo-of-car-on-road-in-city.jpeg?auto=compress&cs=tinysrgb&w=1260&h=750&dpr=2" 
      alt="Luxury car on city street"
      class="w-full h-full object-cover"
    />
  </div>
  
  <div class="container relative z-10 h-full flex flex-col justify-center px-4">
    <div class="max-w-2xl animate-slide-up">
      <h1 class="text-white text-4xl md:text-6xl font-bold mb-4">Drive on Demand</h1>
      <p class="text-white/80 text-xl md:text-2xl mb-8">Rent cars from local owners. Find the perfect vehicle for any occasion.</p>
      
      <div class="bg-white p-6 rounded-lg shadow-lg">
        <form on:submit={handleSearch}>
          <div class="grid grid-cols-1 md:grid-cols-3 gap-4">
            <div>
              <label for="location" class="form-label">Where</label>
              <div class="relative">
                <svg xmlns="http://www.w3.org/2000/svg" class="absolute left-3 top-3 h-5 w-5 text-neutral-500" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M5.05 4.05a7 7 0 119.9 9.9L10 18.9l-4.95-4.95a7 7 0 010-9.9zM10 11a2 2 0 100-4 2 2 0 000 4z" clip-rule="evenodd" />
                </svg>
                <input 
                  type="text" 
                  id="location" 
                  placeholder="City, airport, or address" 
                  bind:value={searchLocation}
                  class="form-input pl-10"
                />
              </div>
            </div>
            <div>
              <label for="start-date" class="form-label">From</label>
              <div class="relative">
                <svg xmlns="http://www.w3.org/2000/svg" class="absolute left-3 top-3 h-5 w-5 text-neutral-500" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M6 2a1 1 0 00-1 1v1H4a2 2 0 00-2 2v10a2 2 0 002 2h12a2 2 0 002-2V6a2 2 0 00-2-2h-1V3a1 1 0 10-2 0v1H7V3a1 1 0 00-1-1zm0 5a1 1 0 000 2h8a1 1 0 100-2H6z" clip-rule="evenodd" />
                </svg>
                <input 
                  type="date" 
                  id="start-date" 
                  bind:value={searchStartDate}
                  class="form-input pl-10 w-full"
                />
              </div>
            </div>
            <div>
              <label for="end-date" class="form-label">Until</label>
              <div class="relative">
                <svg xmlns="http://www.w3.org/2000/svg" class="absolute left-3 top-3 h-5 w-5 text-neutral-500" viewBox="0 0 20 20" fill="currentColor">
                  <path fill-rule="evenodd" d="M6 2a1 1 0 00-1 1v1H4a2 2 0 00-2 2v10a2 2 0 002 2h12a2 2 0 002-2V6a2 2 0 00-2-2h-1V3a1 1 0 10-2 0v1H7V3a1 1 0 00-1-1zm0 5a1 1 0 000 2h8a1 1 0 100-2H6z" clip-rule="evenodd" />
                </svg>
                <input 
                  type="date" 
                  id="end-date" 
                  bind:value={searchEndDate}
                  class="form-input pl-10 w-full"
                />
              </div>
            </div>
          </div>
          <button type="submit" class="mt-4 btn btn-primary w-full md:w-auto">Find Cars</button>
        </form>
      </div>
    </div>
  </div>
</section>