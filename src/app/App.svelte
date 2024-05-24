<script lang="ts">
  const DEFAULT_DATA = {
    href: "",
    imgSrc: "",
  }

  const days = {
    0: 'Lunes',
    1: 'Martes',
    2: 'Miercoles',
    3: 'Jueves',
    4: 'Viernes',
    5: 'Sabado',
    6: 'Domingo',
  }

  const data = {
    '06': {
      href: "https://www.instagram.com/reel/C5etbxhs-fN",
      imgSrc: "/publicaciones/abril/06.png",
    },
    '010': {
      href: "https://www.instagram.com/p/C5oi80DP60w",
      imgSrc: "/publicaciones/abril/010.png",
    },
    '011': {
      href: "https://www.instagram.com/p/C5qoAeXOJ11",
      imgSrc: "/publicaciones/abril/011.png",
    },
    '013': {
      href: "https://www.instagram.com/p/C5w3SnQuJtC",
      imgSrc: "/publicaciones/abril/010.png",
    },
    '014': {
      href: "https://www.instagram.com/p/C5yOmqxOcXi",
      imgSrc: "/publicaciones/abril/014.png",
    },
    '016': {
      href: "https://www.instagram.com/reel/C54BOtzvBnM",
      imgSrc: "/publicaciones/abril/016.png",
    },
    '017': {
      href: "https://www.instagram.com/p/C56rdSivx",
      imgSrc: "/publicaciones/abril/017.png",
    },
    '018': {
      href: "https://www.instagram.com/reel/C59OeVASa6g",
      imgSrc: "/publicaciones/abril/018.png",
    },
    '022': {
      href: "https://www.instagram.com/p/C6HhdhsvjHE",
      imgSrc: "/publicaciones/abril/022.png",
    },
    '023': {
      href: "https://www.instagram.com/p/C6Jyw8Cvvmd",
      imgSrc: "/publicaciones/abril/023.png",
    },
    '024': {
      href: "https://www.instagram.com/reel/C6MowNDuua9",
      imgSrc: "/publicaciones/abril/024.png",
    },
    '025': {
      href: "https://www.instagram.com/p/C6OySe3ud6h",
      imgSrc: "/publicaciones/abril/025.png",
    },
    '028': {
      href: "https://www.instagram.com/reel/C6WfADMxMlz",
      imgSrc: "/publicaciones/abril/028.png",
    },
    '029': {
      href: "https://www.instagram.com/p/C6ZW_hsPFYl",
      imgSrc: "/publicaciones/abril/029.png",
    },
    '118': {
      href: "",
      imgSrc: "/publicaciones/abril/010.png",
    },
  }

  const posts = Object.keys(data).length
  // const imagesPosts = 48

  const months = [
    {
      id: 0,
      days: 30,
      name: 'Abril',
      startDay: 0,
    },
    {
      id: 1,
      days: 31,
      name: 'Mayo',
      startDay: 2,
    },
  ]
  
  let currentMonthIndex = 0
  let activeButtonId = '06' as keyof typeof data

  $: currentMonth = months[currentMonthIndex]

  $: currentData = data[activeButtonId] ?? DEFAULT_DATA

  $: header = Array.from({length: 7}, (_, index) => {
    const {startDay} = currentMonth
    const dayIndex = (startDay + index) % 7 as keyof typeof days
    return days[dayIndex]
  })

  $: cells = Array.from({length:currentMonth.days}, (_, index) => {
    const dataId = currentMonth.id.toString() + index.toString() as keyof typeof data
    const hasContent = data[dataId] != null
    return {
      title: index + 1,
      hasContent: hasContent,
      dataId: dataId,
    }
  })

  const handleIncrementMonth = () => {
    if (currentMonthIndex < months.length - 1) currentMonthIndex++
    activeButtonId = '06'
  }

  const handleDecrementMonth = () => {
    if (currentMonthIndex > 0) currentMonthIndex--
  }

  const handleDataClicked = (event: MouseEvent) => {
    const button = event.currentTarget! as HTMLButtonElement
    const dataId = button.getAttribute('data-id') as keyof typeof data
    activeButtonId = dataId
  }
</script>

<section class="max-w-6xl mx-auto py-4 px-6 md:px-0">
  <h1 class="text-center text-2xl md:text-4xl mb-12 text-sky-600 font-bold uppercase">Publicaciones hechas por Suads para <br class="hidden md:block"> Lighthouse en 2024</h1>
  
  <div class="grid grid-cols-1 md:grid-cols-2 gap-12 mb-4">
    <div>
      <div class="flex justify-between items-center mb-4">
        <button on:click={handleDecrementMonth}>
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="text-sky-600 h-8">
            <path fill="currentColor" d="M9.4 233.4c-12.5 12.5-12.5 32.8 0 45.3l160 160c12.5 12.5 32.8 12.5 45.3 0s12.5-32.8 0-45.3L109.2 288 416 288c17.7 0 32-14.3 32-32s-14.3-32-32-32l-306.7 0L214.6 118.6c12.5-12.5 12.5-32.8 0-45.3s-32.8-12.5-45.3 0l-160 160z"/>
          </svg>
        </button>
        <h2 class="text-center text-lg md:text-xl text-sky-600 font-bold uppercase">{currentMonth.name}</h2>
        <button on:click={handleIncrementMonth}>
          <svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 448 512" class="text-sky-600 h-8">
            <path fill="currentColor" d="M438.6 278.6c12.5-12.5 12.5-32.8 0-45.3l-160-160c-12.5-12.5-32.8-12.5-45.3 0s-12.5 32.8 0 45.3L338.8 224 32 224c-17.7 0-32 14.3-32 32s14.3 32 32 32l306.7 0L233.4 393.4c-12.5 12.5-12.5 32.8 0 45.3s32.8 12.5 45.3 0l160-160z"/>
          </svg>
        </button>
      </div>
      <div class="grid grid-cols-7 mb-4">
        {#each header as title}
          <p class="text-white font-bold text-center capitalize">{title}</p>
        {/each}
      </div>
      <div class="grid grid-cols-7 place-items-center gap-2">
        {#each cells as {title, hasContent, dataId} (dataId)}
        <div class="hover:bg-slate-500 rounded">
          <button data-id="{dataId}" on:click={handleDataClicked} class="flex flex-col justify-center items-center cursor-pointer aspect-square w-[64px] rounded {dataId === activeButtonId ? "bg-slate-400" : ""}">
            <p class="text-white text-center">{title}</p>
            {#if hasContent}
              <div class="h-[20px] aspect-square bg-sky-600"></div>
            {:else}
              <div class="h-[20px] aspect-square bg-transparent"></div>
            {/if}
          </button>
        </div>
        {/each}
      </div>
    </div>

    <div class="flex flex-col justify-between">
      {#if !currentData.imgSrc && !currentData.href}
        <p class="text-white">Sin publicacion esta fecha</p>
      {:else}
        <img src="{currentData.imgSrc}" alt="publicacion" class="">
        <a target="_blank" href="{currentData.href}" class="text-sky-600 hover:underline mt-6">Enlace a la publicación</a>
      {/if}
    </div>
  </div>

  <div>
    <p class="text-white">Total publicaciones: <span class="text-sky-600">{posts}</span></p>
    <!-- <p class="text-white">Total de imagenes publicadas: <span class="text-sky-600">{imagesPosts}</span></p> -->
  </div>
</section>