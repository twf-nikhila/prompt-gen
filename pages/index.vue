<template>
    <div class="p-8 w-full bg-white rounded-lg border border-gray-200 shadow-md sm:p-6 md:p-8 dark:bg-gray-800 dark:border-gray-700">

  <form action="" class="space-y-6">

    <div>
      <label for="image_of" class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300">Image of</label>

      <div class="relative mt-1">
        <input
          type="text"
          id="image_of"
          v-model="image_of"
          class="block p-4 w-full text-gray-900 bg-gray-50 rounded-lg border border-gray-300 sm:text-md focus:ring-blue-500 focus:border-blue-500 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          placeholder="Girl working on laptop, Mountains, Online zoom conference"
        autofocus="autofocus"
        />
      </div>
    </div>

    <div>
      <label for="background" class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-300">Background</label>

      <div class="relative mt-1">
        <input
          type="text"
          id="background"
          v-model="background"
          class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500"
          placeholder="(optional) Specify background color or object"
        />
      </div>
    </div>
    

    <div class="grid gap-6 mb-6 md:grid-cols-2">
        
    <div>
        <label for="selected_style" class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-400">Style</label>
        <select id="selected_style" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" v-model="selected_style">
            <option value="">None</option>
            <option v-for="style in styles" :value="style">{{ style }}</option>
        </select>
    </div>

    <div>
    <label for="selected_modifiers" class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-400">Modifiers (select multiple)</label>
    <select multiple id="selected_modifiers" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" v-model="selected_modifiers">
        <option value="">None</option>
        <option v-for="modifier in modifiers" :value="modifier">
        {{ modifier }}
      </option>
    </select>
    </div>

    <div>
    <label for="selected_time" class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-400">Time</label>
    <select id="selected_time" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" v-model="selected_time">
        <option value="">Let AI Decide</option>
        <option v-for="time in times" :value="time">{{ time }}</option>
    </select>
</div>

    <div>
    <label for="selected_light" class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-400">Light</label>
    <select id="selected_light" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" v-model="selected_light">
        <option value="">Let AI Decide</option>
        <option v-for="light in lights" :value="light">{{ light }}</option>
    </select>
</div>

<div>
    <label for="selected_colors" class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-400">Colors</label>
    <select id="selected_colors" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" v-model="selected_colors">
        <option value="">Let AI Decide</option>
        <option v-for="color in colors" :value="color">{{ color }}</option>
    </select>
</div>

<div>
    <label for="selected_artist" class="block mb-2 text-sm font-medium text-gray-900 dark:text-gray-400">Artist</label>
    <select id="selected_artist" class="bg-gray-50 border border-gray-300 text-gray-900 text-sm rounded-lg focus:ring-blue-500 focus:border-blue-500 block w-full p-2.5 dark:bg-gray-700 dark:border-gray-600 dark:placeholder-gray-400 dark:text-white dark:focus:ring-blue-500 dark:focus:border-blue-500" v-model="selected_artist">
        <option value="">Let AI Decide</option>
        <option v-for="artist in artists" :value="artist">{{ artist }}</option>
    </select>    
</div>
</div>

    <button type="button" class="text-white bg-gradient-to-br from-purple-600 to-blue-500 hover:bg-gradient-to-bl focus:ring-4 focus:outline-none focus:ring-blue-300 dark:focus:ring-blue-800 font-medium rounded-lg text-sm px-5 py-2.5 text-center mr-2 mb-2" @click="generate_prompt">Generate Prompt</button>


    <h2 class="mb-4 text-2xl font-extrabold tracking-tight leading-none text-gray-900 md:text-4xl lg:text-4xl dark:text-white text-center"><span class="text-blue-600 dark:text-blue-500 normal-case" id="prompt">{{prompt}}</span> 

        <button title="Copy Prompt" type="button" class="text-blue-700 border border-blue-700 hover:bg-blue-700 hover:text-white focus:ring-4 focus:outline-none focus:ring-blue-300 font-medium rounded-full text-sm p-2.5 text-center inline-flex items-center dark:border-blue-500 dark:text-blue-500 dark:hover:text-white dark:focus:ring-blue-800" @click="copy_prompt" v-if="prompt.length > 0">
        <svg aria-hidden="true" class="w-5 h-5" fill="currentColor" viewBox="0 0 20 20" xmlns="http://www.w3.org/2000/svg"><path fill-rule="evenodd" d="M10.293 3.293a1 1 0 011.414 0l6 6a1 1 0 010 1.414l-6 6a1 1 0 01-1.414-1.414L14.586 11H3a1 1 0 110-2h11.586l-4.293-4.293a1 1 0 010-1.414z" clip-rule="evenodd"></path></svg>
        <span class="sr-only">Copy</span>
        </button>
    </h2>

    <p class="max-w-md mx-auto mt-5 text-center text-gray-500">
        Made by <a href="https://twitter.com/HeyNikhila" class="font-medium text-blue-600 dark:text-blue-500 hover:underline">@heyNikhila</a>. <br/>
        Help me improve this DM on twitter with your feedback & suggestions. - V0.1<br/>
    </p>

  </form>
  </div>
</template>

<script>
export default {
  name: "IndexPage",
  data() {
    return {
      styles: [
        "Abstract Painting",
        "Acrylic Painting",
        "Action Painting",
        "Aestheticism Painting",
        "Anamorphosis Painting",
        "Art Deco Painting",
        "Art nouveau Painting",
        "Ashcan School Painting",
        "Baroque Painting",
        "Body Painting",
        "Canvas Painting",
        "Cartoon Painting",
        "Chalk Painting",
        "Child's Finger Painting",
        "Chinese Painting",
        "Classicism Painting",
        "Collage Painting",
        "Cubism Painting",
        "Dadaism Painting",
        "De Stijl Painting",
        "Der Blaue Painting",
        "Digital Painting",
        "Drip Painting",
        "Enamel Painting",
        "Encaustic Painting",
        "Expressionism Painting",
        "Figurativism Painting",
        "Fingerpainting Painting",
        "Finger Painting",
        "Fresco Secco Painting",
        "Futurism Painting",
        "Genre Painting",
        "Glitter Glue Painting",
        "Gothic Painting",
        "Gouache Painting",
        "History Painting",
        "Hot Wax Painting",
        "Impressionism Painting",
        "Ink Wash Painting",
        "Japanese Painting",
        "Korean Painting",
        "Landscape Painting",
        "Leaf Painting",
        "Marker Painting",
        "Matte Painting",
        "Miniature Painting",
        "Modernism Painting",
        "Mughal Painting",
        "Mural Painting",
        "Oil Painting",
        "Pastel Painting",
        "Pattachitra Painting",
        "Photorealism Painting",
        "Rajasthan Painting",
        "Realism Painting",
        "Reverse Glass Painting",
        "Sand Painting",
        "Speed Painting",
        "Spray Painting",
        "Still Life Painting",
        "Surrealism Painting",
        "Tanjore Painting",
        "Tempera Painting",
        "Velvet Painting",
        "Watercolor Painting",
        "Anime Art",
        "Bedazzled Art Style",
        "Button Art",
        "Chalk Art",
        "Comic Book Art",
        "Conceptual Art",
        "Leather Art Style",
        "Line Art",
        "Marble Art",
        "Pop Art painting",
        "Portrait Art",
        "Sand Art",
        "Street Art",
        "Woven Art",
        "Anime Style",
        "Atari 2600 Style",
        "Bauhaus Style",
        "Coloring Book Style",
        "Constructivism Style",
        "Fauvism Style",
        "Glitter Style",
        "GTAV Style",
        "NES Style",
        "Retro Comic Book Style",
        "SNES Style",
        "Studio Ghibli Style",
        "Woodburning Style",
        "Woodcut Style",
        "Ballpoint Pen Drawing",
        "Blue Ballpoint Pen Drawing",
        "Colored Pencil Drawing",
        "Pencil Drawing",
        "Red Ballpoint Pen Drawing",
        "Comic Book Cover",
        "Comic Book",
        "Comic Book Panel",
        "Colored Pencil Sketch",
        "Pencil Sketch",
        "3D Render",
        "Boxart",
        "Children's Book",
        "Coloring Book",
        "Copper Plate Engraving",
        "Cross-Stitch",
        "Diamond Engraving",
        "Icon",
        "Linocut",
        "Lowpoly",
        "Old Black and White Photograph",
        "Photograph",
        "Pixelart",
        "Pop Up Book",
        "Ring Engraving",
        "Spray Paint",
        "Stained Glass",
        "Sticker",
        "Stone Cut",
      ],

      artists: [
        "Agnes Lawrence Pelton",
        "Akihito Yoshida",
        "Alex Grey",
        "Alexander Jansson",
        "Alphonse Mucha",
        "Andy Warhol",
        "Artgerm",
        "Asaf Hanuka",
        "Aubrey Beardsley",
        "Banksy",
        "Beeple",
        "Ben Enwonwu",
        "Bob Eggleton",
        "Caravaggio Michelangelo Merisi",
        "Caspar David Friedrich",
        "Chris Foss",
        "Claude Monet",
        "Dan Mumford",
        "David Mann",
        "Diego Velázquez",
        "Disney Animation Studios",
        "Édouard Manet",
        "Esao Andrews",
        "Frida Kahlo",
        "Gediminas Pranckevicius",
        "Georgia O'Keeffe",
        "Greg Rutkowski",
        "Gustave Doré",
        "Gustave Klimt",
        "H.R. Giger",
        "Hayao Miyazaki",
        "Henri Matisse",
        "HP Lovecraft",
        "Ivan Shishkin",
        "Jack Kirby",
        "Jackson Pollock",
        "James Jean",
        "Jim Burns",
        "Johannes Vermeer",
        "John William Waterhouse",
        "Katsushika Hokusai",
        "Kim Tschang Yeul",
        "Ko Young Hoon",
        "Leonardo da Vinci",
        "Lisa Frank",
        "M.C. Escher",
        "Mahmoud Saïd",
        "Makoto Shinkai",
        "Marc Simonetti",
        "Mark Brooks",
        "Michelangelo",
        "Pablo Picasso",
        "Paul Klee",
        "Peter Mohrbacher",
        "Pierre-Auguste Renoir",
        "Pixar Animation Studios",
        "Rembrandt",
        "Richard Dadd",
        "Rossdraws",
        "Salvador Dalí",
        "Sam Does Arts",
        "Sandro Botticelli",
        "Ted Nasmith",
        "Ten Hundred",
        "Thomas Kinkade",
        "Tivadar Csontváry Kosztka",
        "Victo Ngai",
        "Vincent Di Fate",
        "Vincent van Gogh",
        "Wes Anderson",
        "wlop",
        "Yoshitaka Amano",
      ],

      modifiers: [
        "cinematic",
        "hd",
        "4k",
        "8k",
        "3d",
        "4d",
        "highly detailed",
        "octane render",
        "trending artstation",
        "Pixelate",
        "Blur",
        "Beautiful",
        "Very Beautiful",
        "Very Very Beautiful",
      ],
      times: [
        "futuristic",
        "modern",
        "ancient",
        "antique",
        "Retro",
        "old-fashioned",
        "youthful",
      ],
      lights: [
        "daylight",
        "moonlight",
        "natural light",
        "Front Light",
        "Backlight",
        "Soft Light",
        "Hard Light",
      ],
      colors: ["colorful", "Black and white", "Greyscale"],

      //material: ["glass", "sand", "wood"]
      //texture

      selected_style: "",
      selected_artist: "",
      selected_modifiers: [],
      selected_time: "",
      selected_light: "",
      selected_colors: "",

      image_of: "",
      background: "",
      prompt: "",
    };
  },

  methods: {
    copy_prompt() {
        var r = document.createRange();
r.selectNode(document.getElementById('prompt'));
window.getSelection().removeAllRanges();
window.getSelection().addRange(r);
document.execCommand('copy');
window.getSelection().removeAllRanges();
    },

    generate_prompt() {
      if (this.image_of == "") {
        alert("Enter description of image");
        return false;
      }

      this.prompt = "";

      if (this.selected_modifiers.length > 0) {
        var temp = this.selected_modifiers
          .filter(function (str) {
            return str.indexOf("Beautiful") > -1;
          })
          .join(" ");
        console.log(temp);

        if (temp.length > 0) {
          this.prompt += temp;
        }
      }

      if (this.selected_time) {
        this.prompt += " " + this.selected_time;
      }

      if (this.selected_style) {
        this.prompt += " " + this.selected_style + " of a";
      }

      this.prompt += " " + this.image_of;

      if (this.background) {
        this.prompt += " with background " + this.background;
      }

      if (this.selected_artist) {
        this.prompt += " by " + this.selected_artist;
      }

      if (this.selected_modifiers.length > 0) {
        var temp = this.selected_modifiers
          .filter(function (str) {
            return str.indexOf("Beautiful") === -1;
          })
          .join(" ");

        if (temp.length > 0) {
          this.prompt += " , " + temp;
        }
      }

      if (this.selected_light) {
        this.prompt += ", " + this.selected_light;
      }

      if (this.selected_colors) {
        this.prompt += ", " + this.selected_colors;
      }

      console.log(this.prompt);
    },
  },
};
</script>
