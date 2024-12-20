<template>
  <head>
    <meta
      name="description"
      content="Portfolio of [Your Name], showcasing projects and skills for attachment opportunities."
    />
    <meta name="keywords" content="Portfolio, Projects, Developer, Attachment, Resume" />
  </head>
  <div :class="{ dark: darkMode }" id="app">
    <!-- Navigation Bar -->
    <nav>
      <ul>
        <li><a href="#hero">Home</a></li>
        <li><a href="#about">About</a></li>
        <li><a href="#portfolio">Portfolio</a></li>
        <li><a href="#contact">Reach Out</a></li>
      </ul>
      <div class="column">
        <button class="download-resume" @click="downloadResume">Resume</button>
        <span style="width: 10px"></span>
        <button
          @click="darkMode = !darkMode"
          :class="{ 'buttonText-light': !darkMode, 'buttonText-dark': darkMode }"
          class="theme-toggle-button"
        >
          {{ darkMode ? 'Light Mode' : 'Dark Mode' }}
        </button>
      </div>
    </nav>

    <!--Spacer section
    pushes the hero section below the floating nav
    making all its heading visible-->
    <section id="hero" style="height: 8px"></section>
    <!-- Hero Section -->
    <section class="hero">
      <h1>Welcome to My Portfolio</h1>
      <p>Your tagline or introduction goes here.</p>
    </section>

    <!--Spacer section
    pushes the about section below the floating nav
    making all its heading visible-->
    <section id="about" style="height: 8px"></section>
    <!-- About Section -->
    <section class="about">
      <h2>About Me</h2>
      <p>
        I'm a passionate developer/designer/creator with experience in web and application
        development.
      </p>
    </section>

    <!--Spacer section
    pushes the portfolio section below the floating nav
    making all its heading visible-->
    <section id="portfolio" style="height: 8px"></section>
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
    <div v-if="selectedProject" class="modal">
      <div class="modal-content">
        <span class="close" @click="selectedProject = null">&times;</span>
        <h3>{{ selectedProject.title }}</h3>
        <column class="column">
          <img :src="selectedProject.image" :alt="selectedProject.title" class="imageViewSize" />
          <p class="imageViewSize">{{ selectedProject.description }}</p>
        </column>
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
    <section id="contact" style="height: 8px"></section>
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
        <a href="https://linkedin.com/in/username" target="_blank">LinkedIn</a>
      </row>
    </footer>
  </div>
</template>

<script>
export default {
  data() {
    return {
      portfolioItems: [
        {
          id: 1,
          image: 'src/assets/images/myProject1.jpeg',
          title: 'DIY battery Pack',
          description:
            'This project involves designing and building a 2S 3P lithium-ion battery pack suitable for powering RC cars and other DIY electronic projects. The pack combines the benefits of increased voltage (2S) and higher capacity (3P) for optimal performance. It aims to promote sustainability by repurposing 18650 Li-ion cells salvaged from damaged or unused devices. By reusing batteries, we reduce electronic waste and make the project cost-effective.',
        },
        {
          id: 2,
          image: 'project2.jpg',
          title: 'Project Two',
          description: 'A detailed description of project two.',
        },
        {
          id: 3,
          image: 'project3.jpg',
          title: 'Project Three',
          description: 'A detailed description of project three.',
        },
      ],

      skills: [
        { name: 'HTML', level: 90 },
        { name: 'CSS', level: 85 },
        { name: 'JavaScript', level: 80 },
        { name: 'Vue.js', level: 75 },
        { name: 'Python', level: 70 },
        { name: 'Flutter', level: 60 },
      ],

      form: {
        name: '',
        email: '',
        message: '',
      },
      testimonials: [
        { id: 1, text: 'Amazing work, highly recommended!', author: 'John Doe' },
        { id: 2, text: 'Very professional and creative.', author: 'Jane Smith' },
      ],
      selectedProject: null,
      darkMode: false,
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
      window.open(
        'https://drive.google.com/file/d/1zrzmuao6mwdxKtOVfyPp__gH5UPjxklv/view?usp=sharing',
        '_blank',
      )
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
  max-width: 100%;
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

/* Navigation Bar */
nav {
  /*position: absolute;*/
  top: 0;
  /*left: 5%;*/
  width: inherit;
  background: white;
  display: flex;
  justify-content: space-between;
  padding: 10px 20px;
  box-shadow: 0 5px 40px rgba(0, 0, 0, 0.1);
  z-index: 1000;
  align-self: center;
  position: sticky;
  transition: color 0.3s ease-in-out;
  border-style: inset;
  border-right: none;
  border-bottom: none;
}

nav ul {
  display: flex;
  list-style: none;
  margin: 0;
  padding: 0;
}

nav ul li:hover {
  transform: scale(1.1);
  transition: transform 0.3s ease;
}

nav a {
  margin: 0 15px;
  text-decoration: none;
  color: #333;
}

nav a:hover {
  text-decoration: underline;
  color: #58a6ff;
  transform: scale(1.05);
  transition: transform 0.3s ease;
}

/* Theme Toggle */
.theme-toggle-button {
  background: none;

  padding: 5px 10px;
  border-radius: 5px;
}

.theme-toggle-button:hover {
  transform: scale(1.05);
  transition: transform 0.3s ease;
}

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
}

.modal-content {
  background: white;
  padding: 20px;
  text-align: center;
  position: relative;
}

.modal-content .close {
  position: absolute;
  top: 10px;
  right: 10px;
  cursor: pointer;
}

.imageSize {
  max-width: 150px;
  max-height: 150px;
}

.imageViewSize {
  max-width: 450px;
  max-height: 450px;
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

.column {
  display: flex;
  justify-content: space-around;
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

.dark .download-resume {
  /*background: black;*/
  color: rgb(220, 215, 215);
  border-color: rgb(220, 215, 215);
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

/* Responsive Design */
@media (max-width: 768px) {
  .portfolio-grid {
    grid-template-columns: 1fr;
  }

  nav ul {
    flex-direction: column;
  }
}
</style>
