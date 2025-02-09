<template>
  <div :class="{ dark: darkMode }" id="app">
    <!-- Navigation Bar -->
    <nav>
      <div class="nav-container">
        <!-- Brand Name or Logo -->
        <div class="brand">
          <a href="#hero" @click="toggleMenu">MyPortfolio</a>
        </div>

        <!-- Hamburger Menu (Visible on small screens) -->
        <button class="hamburger" @click="toggleMenu" aria-label="Toggle Menu">
          <span :class="{ open: isMenuOpen }"></span>
          <span :class="{ open: isMenuOpen }"></span>
          <span :class="{ open: isMenuOpen }"></span>
        </button>

        <!-- Navigation Links -->

        <ul :class="{ 'nav-links': true, open: isMenuOpen }">
          <div class="nav-menu">
            <li><a href="#hero" @click="closeMenu">Home</a></li>
            <li><a href="#about" @click="closeMenu">About</a></li>
            <li><a href="#portfolio" @click="closeMenu">Portfolio</a></li>
            <li><a href="#contact" @click="closeMenu">Reach Out</a></li>
            <li><a href="#" @click="(downloadResume(), closeMenu())">Resume</a></li>
          </div>
          <!-- Resume and Theme Toggle -->
          <div class="nav-actions">
            <!--<button class="download-resume" @click="(downloadResume(), closeMenu())">Resume</button>-->
            <!--<button
              @click="((darkMode = !darkMode), closeMenu())"
              :class="{ 'buttonText-light': !darkMode, 'buttonText-dark': darkMode }"
              class="theme-toggle-button"
            >
              {{ darkMode ? 'Light Mode' : 'Dark Mode' }}
            </button>-->
            <button @click="darkMode = !darkMode" class="theme-toggle">
              <Moon v-if="!darkMode" class="icon" />
              <Sun v-else class="icon" />
            </button>
          </div>
        </ul>
      </div>
    </nav>

    <!--Spacer section
    pushes the hero section below the floating nav
    making all its heading visible-->
    <section id="hero" style="height: 15px"></section>
    <!-- Hero Section -->
    <section class="hero">
      <h1>Welcome to My Portfolio</h1>
      <p>
        I am driven by curiosity and a passion for hands-on projects. I enjoy using tools like
        Fusion 360, Tinkercad, Codewars, and SkillsBuild to turn creative ideas into functional
        designs. Whether it’s app development or engineering design, I am fascinated by the process
        of bringing ideas to life and will deliver exceptional results. Outside of work, I stay
        active through swimming, cycling and working out. I also enjoy building meaningful
        connections, fostering a supportive community with my colleagues on campus.
      </p>
    </section>

    <!--Spacer section
    pushes the about section below the floating nav
    making all its heading visible-->
    <section id="about" style="height: 15px"></section>
    <!-- About Section -->
    <section class="about">
      <h2>About Me</h2>
      <p>
        I'm an aspiring mechatronics engineer, in my third year of studies at Jomo Kenyatta
        University of Agriculture and Technology
      </p>
    </section>

    <!--Spacer section
    pushes the portfolio section below the floating nav
    making all its heading visible-->
    <section id="portfolio" style="height: 15px"></section>
    <!-- Portfolio Section -->
    <section>
      <h2>My Work</h2>
      <div class="portfolio-grid">
        <div
          class="portfolio-item"
          v-for="item in portfolioItems"
          :key="item.id"
          @click="openModal(item)"
        >
          <img :src="item.image" :alt="item.title" class="imageSize" />
          <h3>{{ item.title }}</h3>
        </div>
      </div>
    </section>

    <!-- Modal for Portfolio Items -->
    <!--
    <div v-if="selectedProject" class="modal">
      <div class="modal-content">
        <row class="modal-head">
          <h3>{{ selectedProject.title }}</h3>
          <span class="close" @click="selectedProject = null">&times;</span>
        </row>
        <column class="column">
          <img :src="selectedProject.image" :alt="selectedProject.title" class="imageSize" />
          <p class="imageViewSize">{{ selectedProject.description }}</p>
        </column>
      </div>
    </div>
  -->
    <div v-if="selectedProject" class="modal-overlay">
      <div class="modal" @scroll="handleScroll" ref="modalContent">
        <div class="modal-content">
          <div class="modal-head">
            <h3>{{ selectedProject.title }}</h3>
            <span class="close" @click="selectedProject = null">&times;</span>
          </div>
          <div class="modal-body">
            <img :src="selectedProject.image" :alt="selectedProject.title" class="imageSize" />
            <p class="imageViewSize" v-html="selectedProject.description"></p>
          </div>
        </div>
      </div>
    </div>

    <!--Skills Section-->
    <section id="skills">
      <h2>Skills</h2>
      <div v-for="skill in skills" :key="skill.name" class="skill">
        <!--<span>{{ skill.name }}</span>
        <div class="skill-bar" :style="{ width: skill.level + '%' }"></div>-->
        <div class="skill-label">
          <span>{{ skill.name }}</span>
          <!--<span class="skill-level">{{ skill.level }}%</span>-->
        </div>
        <div class="skill-bar">
          <div class="skill-bar-value" :style="{ width: skill.level + '%' }"></div>
        </div>
        <span class="skill-level">{{ skill.level }}%</span>
      </div>
    </section>

    <!--Spacer section
    pushes the contacct section below the floating nav
    making all its heading visible-->
    <section id="contact" style="height: 15px"></section>
    <!-- Contact Section -->
    <section id="contact1">
      <h2>Contact Me</h2>
      <form @submit.prevent="handleSubmit">
        <label for="name">Name</label>
        <input type="text" id="name" v-model="form.name" required />

        <label for="email">Email</label>
        <input type="email" id="email" v-model="form.email" required />

        <label for="message">Message</label>
        <textarea id="message" v-model="form.message" required></textarea>

        <button type="submit" class="form-button">Send</button>
      </form>
    </section>

    <!--Testimonials Section-->
    <section id="testimonials">
      <h2>Testimonials</h2>
      <div class="carousel">
        <div v-for="testimonial in testimonials" :key="testimonial.id" class="testimonial-item">
          <p>"{{ testimonial.text }}"</p>
          <h4>- {{ testimonial.author }}</h4>
        </div>
      </div>
    </section>

    <!-- Footer -->
    <footer>
      <h2>Find Me Online</h2>
      <row style="display: flex; justify-content: space-around" class="row">
        <a href="https://github.com/alexpxcell" target="_blank">GitHub</a>
        <a href="https://linkedin.com/in/alex-wandugu-a6250226b" target="_blank">LinkedIn</a>
        <a
          href="https://web.facebook.com/people/Alex-Thiongo/pfbid0k43xFKtaRk45DkT8Tn3tTnGqQn9Xqb5QNV1r3nadjB2ueBNq1sDwqd9R5RDLFdgol/"
          target="_blank"
          >Facebook</a
        >
      </row>
    </footer>
  </div>
</template>

<script>
import { ref, watch, onMounted } from 'vue'
import { Sun, Moon } from 'lucide-vue-next'

export default {
  components: { Sun, Moon },
  data() {
    return {
      portfolioItems: [
        {
          id: 1,
          image: '/images/myProject1.jpeg',
          title: 'DIY Battery Pack',
          description:
            'This project involves designing and building a 2S 3P lithium-ion battery pack suitable for powering RC cars and other DIY electronic projects.',
        },
        {
          id: 2, // Fixed duplicate ID
          image: '/images/google-developers-logo.png',
          title: 'Google Developers Student',
          description:
            'As a Google Developer Student, I am passionate about leveraging technology for continuous learning. <br> <a href="https://g.dev/alexwandugu" target="_blank" style="color:black;">View My Progress</a>',
        },
      ],
      skills: [
        { name: '2D & 3D design', level: 90 },
        { name: 'Basic Web3 kit', level: 70 },
        { name: 'C++', level: 80 },
        { name: 'Vue', level: 60 },
        { name: 'Python', level: 40 },
        { name: 'Circuit design', level: 40 },
      ],
      form: {
        name: '',
        email: '',
        message: '',
      },
      testimonials: [
        { id: 1, text: 'Amazing work, highly recommended!', author: 'Samuel Otieno' },
        { id: 2, text: 'Very professional and creative.', author: 'Esther Wangui' },
      ],
      selectedProject: null,
      darkMode: false,
      isMenuOpen: false,
      startTouch: 0,
    }
  },
  methods: {
    openModal(item) {
      this.selectedProject = item
    },
    handleSubmit() {
      if (this.form.name && this.form.email && this.form.message) {
        this.isSubmitting = true
        setTimeout(() => {
          alert('Your message has been sent!')
          this.isSubmitting = false
          this.form = { name: '', email: '', message: '' }
        }, 2000)
      } else {
        alert('Please fill out all fields.')
      }
    },
    downloadResume() {
      alert('Opening new tab to view my resume')
      window.open(
        'https://drive.google.com/file/d/16SNvbIeKU0QvgXDkZflvtSLW4hAXuemw/view?usp=sharing',
        '_blank',
      )
    },
    toggleMenu() {
      this.isMenuOpen = !this.isMenuOpen
    },
    closeMenu() {
      this.isMenuOpen = false
    },
    handleScroll() {
      const modal = this.$refs.modalContent
      if (modal.scrollTop + modal.clientHeight >= modal.scrollHeight) {
        console.log('Reached the bottom of the modal.')
      }
    },
  },
  created() {
    const savedTheme = localStorage.getItem('theme')
    this.darkMode = savedTheme === 'dark'
  },
  watch: {
    darkMode(newValue) {
      localStorage.setItem('theme', newValue ? 'dark' : 'light')
      document.body.classList.toggle('dark', newValue)
    },
  },
}
</script>

<style scoped>
/* General Styles */
#app {
  font-family: Arial, sans-serif;
  line-height: 1.6;
  /*color: #333;*/
  max-width: 100vw;
  margin: 0px;
  padding: 20px;
}

section {
  margin-bottom: 40px;
}

h1,
h2 {
  text-align: center;
}

button {
  cursor: pointer;
}

.buttonText-light {
  color: black;
  border: 1px solid #333;
}

.buttonText-dark {
  color: white;
  border: 1px solid #f4f1f1;
}

nav {
  background: white;
  box-shadow: 0 5px 40px rgba(0, 0, 0, 0.1);
  position: sticky;
  top: 0;
  z-index: 1000;
  padding: 10px 20px;
}

.nav-container {
  display: flex;
  justify-content: space-between;
  align-items: center;
}

.nav-container :hover {
  outline: none;
}

.brand a {
  font-size: 1.5rem;
  font-weight: bold;
  text-decoration: none;
  color: #333;
}

/* Hamburger Menu */
.hamburger {
  display: none;
  flex-direction: column;
  justify-content: space-between;
  width: 30px;
  height: 30px;
  border: none;
  background: transparent;
  cursor: pointer;
  z-index: 1200;
  outline: none;
}

.hamburger span {
  display: block;
  height: 4px;
  width: 100%;
  border-radius: 4px;
  background: #333;
  transition: transform 0.4s ease;
}

.hamburger span.open:nth-child(1) {
  transform: rotate(46deg) translate(5.5px, 12px);
  width: 100%;
  translate: 27%;
}

.hamburger span.open:nth-child(2) {
  transform: rotate(312deg) translate(-4px, -3.5px);
  width: 100%;
  translate: 27%;
  background-color: #58a6ff;
}

.hamburger span.open:nth-child(3) {
  transform: rotate(312deg) translate(5px, -11.6px);
  width: 100%;
  translate: 27%;
}

/* Navigation Links */
.nav-links {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
}

.nav-links li {
  margin: 0 15px;
}

.nav-links a {
  text-decoration: none;
  color: #333;
  font-size: 1rem;
  transition: font 0.4s ease;
}

.nav-links a:hover {
  color: #58a6ff;
  font-size: larger;
}

.nav-menu {
  display: flex;
  flex-direction: row;
}

.nav-actions {
  display: flex;
  gap: 10px;
}

.theme-toggle {
  background: transparent;
  border: none;
  cursor: pointer;
  display: flex;
  align-items: center;
  justify-content: center;
  border-radius: 50%;
  transition: 0.3s ease;
}

.theme-toggle:hover {
  background: rgba(0, 0, 0, 0.1);
  border: #121212 1px solid;
}

.icon {
  width: 18px;
  height: 18px;
  color: black;
}

/* Theme Toggle */
/*.theme-toggle-button {
  background: none;

  padding: 5px 10px;
  border-radius: 5px;
}

.theme-toggle-button:hover {
  transform: scale(1.05);
  transition: transform 0.3s ease;
}*/

.download-resume {
  background: none;
  padding: 5px 10px;
  border-radius: 5px;
}

.download-resume:hover {
  transform: scale(1.05);
  transition: transform 0.3s ease;
}

.hero,
.about {
  border-left: inset;
  padding-left: 10px;
}

/* Portfolio Section */
.portfolio-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 20px;
  border: outset;
  border-left: none;
  border-top: none;
}

.portfolio-item {
  text-align: center;
  cursor: pointer;
}

.portfolio-item:hover {
  transform: scale(1.05);
  transition: transform 0.3s ease;
}

/* Modal Styles */
.modal-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: rgba(0, 0, 0, 0.5);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}

.modal {
  background: white;
  border-radius: 4.1%;
  max-width: 700px;
  max-height: 80%;
  display: flex;
  flex-direction: column;
}

/*
.modal {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(0, 0, 0, 0.8);
  display: flex;
  justify-content: center;
  align-items: center;
  z-index: 1000;
}*/

.modal-head {
  display: flex;
  justify-content: space-between;
  align-items: center;
  position: relative;
}

.modal-head h3 {
  margin-top: 0;
}

.modal-content {
  background: white;
  padding: 20px;
  border-radius: 4%;
  text-align: center;
  position: relative;
}

.modal-content .close {
  cursor: pointer;
  padding: 3%;
  font-size: large;
}

.modal-body {
  display: flex;
  justify-content: space-around;
}

.imageSize {
  max-width: 300px;
  max-height: 300px;
  width: auto;
  height: auto;
}

.imageViewSize {
  max-width: 450px;
  max-height: 450px;
  width: auto;
  height: auto;
}

.customlink {
  color: green !important;
}

.skill {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
  gap: 10px;
  align-items: center;
}

.skill-bar {
  height: 10px;
  max-width: 100%;
  background-color: lightgray;
  border-radius: 4px;
  overflow: hidden;
  position: relative;
}

.skill-level {
  font-size: 0.9rem;
  font-weight: bold;
  margin-left: 10px;
  color: darkgreen;
  opacity: 0;
  transition: opacity 0.1s ease-in-out;
}

.skill-bar:hover + .skill-level {
  opacity: 1;
}

.skill-bar-value {
  height: 10px;
  max-width: 100%;
  background-color: rgb(26, 150, 26);
  border-radius: 4px;
  overflow: hidden;
  position: relative;
  transition: background-color 0.5s ease-in-out;
}

.skill-bar-value:hover {
  background-color: limegreen;
}

.skill-bar:hover .skill-bar-value {
  background-color: limegreen;
}

.skill-label {
  display: flex;
  justify-content: space-between;
  align-items: center;
  margin-bottom: 5px;
}

.skill-label:hover ~ .skill-level {
  opacity: 1;
}

.testimonial-item {
  background: none;
  border-radius: 10px;
  max-width: fit-content;
}

form {
  display: flex;
  flex-direction: column;
}

input {
  border-radius: 5px;
  border-style: double;
}
textarea {
  background: none;
  border-radius: 5px;
  max-width: 100%;
  min-width: 100%;
  min-height: 40px;
}

.form-button {
  max-width: 100px;
  align-self: flex-end;
  margin-top: 10px;
  padding: 5px 10px;
  border-radius: 8px;
}

.form-button:hover {
  transform: scale(1.05);
  transition: transform 0.3s ease;
}

/*footer styling*/
.row a {
  color: rgb(52, 116, 38);
}

/* Dark Mode */
.dark {
  background-color: #121212;
  color: rgb(220, 215, 215);
}

.dark nav {
  background-color: #333;
}

.dark nav a {
  color: rgb(220, 215, 215);
}

.dark .hamburger span {
  background: rgb(220, 215, 215);
}

.dark .nav-links.open {
  background: #333;
}

.dark .download-resume {
  /*background: black;*/
  color: rgb(220, 215, 215);
  border-color: rgb(220, 215, 215);
}

.dark .icon {
  color: white;
}

.dark .theme-toggle:hover {
  border: white 1px solid;
}

.dark .modal-content {
  background-color: rgba(0, 0, 139, 0.767);
}

.dark .skill-level {
  color: limegreen;
}

.dark input,
.dark textarea {
  background-color: grey;
  color: white;
}
.dark .row a {
  color: rgb(58, 165, 33);
}

/* Mobile Styles */
@media (max-width: 773px) {
  .hamburger {
    display: flex;
  }

  .nav-menu {
    display: flex;
    flex-direction: column;
  }

  .nav-links {
    position: absolute;
    top: 60px;
    right: 0;
    width: fit-content;
    height: 100vh;
    background: white;
    flex-direction: column;
    align-items: center;
    display: none;
    padding-right: 10%;
    padding-left: 3%;
    transition: transform 0.3s ease;
  }

  .nav-links.open {
    display: flex;
    transform: translateY(0);
  }

  .nav-links li {
    margin: 15px 0;
  }

  .nav-actions {
    display: flex;
    flex-direction: column;
  }

  .nav-actions .download-resume {
    border: none;
    font-size: medium;
    text-align: start;
    padding-top: 10%;
  }

  .nav-actions .theme-toggle-button {
    border: none;
    font-size: medium;
    padding-top: 10%;
  }
}

@media (max-width: 650px) {
  .modal-body {
    padding: 2px;
    overflow-y: auto;
    flex-direction: column;
  }

  .imageViewSize {
    max-width: 300px;
    max-height: 100px;
    width: auto;
    height: auto;
  }
}
</style>
