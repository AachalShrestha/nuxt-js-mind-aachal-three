<template>
  <div>
    <MouseGradient />
    <!-- Loading State -->
    <div v-if="isLoading" class="flex items-center justify-center h-screen">
      <p>Loading...</p>
    </div>

    <!-- Error State -->
    <div v-else-if="hasError" class="flex items-center justify-center h-screen">
      <p>Error loading settings. Please try again later.</p>
    </div>

    <!-- Main Content -->
    <div v-else class="relative">
      <!-- Background -->
<!--       <div
        class="absolute inset-0 bg-cover bg-center"
        :style="{ backgroundImage: homepageSettings?.thumbnail ? `url(${homepageSettings.thumbnail})` : 'none'}"
      ></div> -->

      <!-- Menu or Drawer -->
      <div class="relative z-10">
          <Drawer />
      </div>
      <div class="container">
        <!-- Title Section -->
        <div class="title-container flex justify-evenly items-center pt-4">
            <div class="flex flex-wrap justify-evenly items-center w-full max-w-6xl px-4">
                <div>
                  <NuxtImg :src="imgSrc" class="pf-img" alt="pf img" loading="lazy"/>
                </div>
              <div class="w-90 lg:w-[50%]">
                <h1 class="text-8xl font-bold mb-4">
                  {{ aboutSettings?.site_title || "About Meeee" }}
                </h1>
                <p>
                  {{ aboutSettings?.description || "About Meeee" }}
                </p>
              </div>
            </div>
        </div>
        <div class="about-content">
          <div class="mt-14">
              <h3>Experience</h3>
              <div class="about-content-container flex gap-12 flex-wrap">
                <div class="about-content-item">
                  <p class="font-medium">Web and Graphic Design Intern</p>
                  <p>OctoSales <br>Jan 24 - Apr 24</p>
                </div>
                <div class="about-content-item">
                  <p class="font-medium">Digital Marketeer Student</p>
                  <p>YOKUU<br>Aug 23 - Nov 23</p>
                </div>
              </div>
          </div>
          <div class="mt-14">
              <h3>Education</h3>
              <div class="about-content-container flex gap-12 flex-wrap">
                <div class="about-content-item">
                  <p class="font-medium">Media & Information Design</p>
                  <p>Luca School of Arts <br>Sept 24 - June 26</p>
                </div>
                <div class="about-content-item">
                  <p class="font-medium">Multimedia & Creative Technologies</p>
                  <p>Erasmus University College Brussels<br>Sept 21 - June 24</p>
                </div>
                <div class="about-content-item">
                  <p class="font-medium">Math and Science</p>
                  <p>Sint-Guido Instituut<br>Sept 15 - June 21</p>
                </div>
              </div>
          </div>
          <div class="mt-14">
              <h3>Soft(ware) skills</h3>
              <div class="about-content-container flex gap-12 flex-wrap">
                <div class="about-content-item">
                  <p class="font-medium">Interactive & Digital Design</p>
                  <ul>
                    <li>Interactive Design (TouchDesigner, Unity, Resolume, MadMapper, Unreal, Ableton Live)</li>
                    <li>Projection Mapping</li>
                    <li>3D modeling & animation (Blender, Maya)</li>
                    <li>Front-End Development (HTML, CSS, JavaScript)</li>
                    <li>UX/UI Design</li>
                  </ul>
                </div>
                <div class="about-content-item">
                  <p class="font-medium">Graphic & Motion Design</p>
                  <ul>
                    <li>Adobe Creative Cloud (Illustrator, Photoshop, Premiere Pro, After Effects)</li>
                    <li>2D & 3D Motion Graphics</li>
                    <li>Video Editing</li>
                    <li>Branding</li>
                    <li>Design Thinking</li>
                  </ul>
                </div>
                <div class="about-content-item">
                  <p class="font-medium">Soft Skills</p>
                  <ul>
                    <li>Creativity</li>
                    <li>Teamwork</li>
                    <li>Flexibility</li>
                    <li>Problem Solving</li>
                    <li>Adaptability</li>
                  </ul>
                </div>
              </div>
          </div>
          <div class="mt-14">
              <h3>Interests</h3>
              <div class="about-content-container flex gap-12 flex-wrap">
                <div class="about-content-item">
                  <p class="font-medium">Crocheting</p>
                  <p>During Covid, I stumbled upon a ball of yarn and a crochet hook that had been sitting untouched in my room. Bored and looking for something to do, I decided to learn the basic stitches—and I haven't stopped since. </p>
                </div>
                <div class="about-content-item">
                  <p class="font-medium">Video editing and Motion Graphics</p>
                  <p>I've always enjoyed editing videos and creating cool effects, even before starting my bachelor’s degree. I love bringing my ideas to life through editing, whether it's crafting special effects or simply putting together vlogs to capture and preserve memories.</p>
                </div>
                <div class="about-content-item">
                  <p class="font-medium">Dancing and filming</p>
                  <p>From a young age, I’ve been passionate about dance. It all began with mimicking dance moves from TV, which soon led to my introduction to Traditional Nepali Dance. Over time, I also developed an interest in K-pop dance covers and even formed a group with some friends. Sometimes, I film and edit our dance videos.</p>
                </div>
              </div>
          </div>
          <div class="mt-14">
              <h3>Special mentions</h3>
              <p class="max-w-[70%]">Every year, the second-year students in our program organize an award show where both the public and professors select the winners.</p>
              <div class="about-content-container flex gap-12 flex-wrap mt-10">
                <div class="about-content-item">
                  <p class="font-medium">Impact award</p>
                  <p>For my bachelor’s work, I received the "Impact Award," which is presented to a final-year project that stands out for its societal relevance and its aim to make a difference in the perception of a social issue. Through an original and innovative multimedia approach, the winner successfully astonishes the audience and leaves a lasting impression.</p>
                </div>
                <div class="about-content-item">
                  <p class="font-medium">Young Potential award</p>
                  <p>An award I received in my first year. This award was given to one the best first year projects.</p>
                </div>
                <div class="about-content-item">
                  <img src="../public/img/award.jpg" class="h-[300px]">
                </div>
              </div>
          </div>
        </div>
        
      </div>
      <MainFooter />
    </div>

    <!-- Load pages -->
	<WorksTable />
  </div>
</template>
<script setup>
import { ref, onMounted } from "vue";
import ColorMode from "~/components/ColorMode.vue";

const colorMode = useColorMode()

// State variables
const aboutSettings = ref(null);
const isLoading = ref(true);
const hasError = ref(false);

const imgSrc = ref("/img/PF_IMG_BLACK.png")
// Fetch JSON data on mount
onMounted(async () => {
  try {
    const response = await fetch("/_data/about.json");

    if (!response.ok) {
      throw new Error("Failed to fetch about settings");
    }

    aboutSettings.value = await response.json();
    isLoading.value = false;
  } catch (error) {
    hasError.value = true;
    console.error("Error loading about settings:", error);
  }
});

watch(
  () => colorMode.preference,
  (newMode) => {
    if(newMode == "light"){
    imgSrc.value = "/img/PF_IMG_BLACK.png";
    }else{
      imgSrc.value = "/img/PF_IMG_WHITE.png";
    }
    console.log(imgSrc)
  }
);

</script>

<style>

.pf-img{
  height: 300px;
  margin-bottom: 15px;
}

.about-content-item{
  width: 330px;
}

.about-content-item p, li{
  font-size: 14px;
}

/* .pf-img {
  width: 300px;
  height: 300px;
  background-image: url('../public/img/PF_IMG_BLACK.png');
  background-size: cover;
  background-position: center;
}

.light-mode .pf-img {
  background-image: url('../public/img/PF_IMG_BLACK.png');
}

.dark-mode .pf-img {
  background-image: url('../public/img/PF_IMG_WHITE.png');
} */
</style>