<template>
  <v-app>
    <!-- Hero Section -->
    <v-parallax
      src="https://images.unsplash.com/photo-1516321318423-f06f85e504b3?ixlib=rb-4.0.3&auto=format&fit=crop&w=1920&q=80"
      height="700"
      class="hero-parallax"
    >
      <div class="hero-overlay"></div>
      <v-row align="center" justify="center" class="fill-height hero-content">
        <v-col cols="12" class="text-center px-4">
          <h1
            class="hero-title animate__animated animate__fadeIn animate__delay-1s"
          >
            SchoolSync Dashboard
          </h1>
          <h4
            class="hero-subtitle animate__animated animate__fadeIn animate__delay-2s"
          >
            Transform your school's operations with our cutting-edge platform
          </h4>
          <v-btn
            color="pink"
            x-large
            rounded
            href="#contact"
            class="hero-btn animate__animated animate__fadeIn animate__delay-3s"
          >
            Get Started
          </v-btn>
        </v-col>
      </v-row>
    </v-parallax>

    <!-- Features Section -->
    <v-container id="features" class="features-section">
      <v-row>
        <v-col cols="12" class="text-center">
          <h2 class="section-title animate__animated animate__fadeInUp">
            What We Offer
          </h2>
          <p
            class="section-subtitle animate__animated animate__fadeInUp animate__delay-1s"
          >
            Powerful tools to streamline your school's workflow
          </p>
        </v-col>
      </v-row>
      <v-row class="features-grid">
        <v-col
          cols="12"
          md="4"
          v-for="(feature, i) in features"
          :key="i"
          class="animate__animated animate__fadeInUp"
          :class="{
            'animate__delay-1s': i === 1,
            'animate__delay-2s': i === 2,
          }"
        >
          <v-card
            class="modern-card mx-auto pa-4"
            max-width="344"
            elevation="0"
          >
            <v-img
              :src="feature.img"
              height="200"
              class="feature-img"
              @click="openImage(feature.img)"
              style="cursor: pointer"
            />
            <v-card-title class="feature-title" style="word-break: break-word">
              {{ feature.title }}
            </v-card-title>
            <v-card-text class="feature-text">
              {{ feature.desc }}
            </v-card-text>
          </v-card>
        </v-col>
      </v-row>
    </v-container>

    <!-- Custom Solutions Section -->
    <v-container id="solutions" fluid class="solutions-section">
      <v-row align="center">
        <v-col cols="12" md="6" class="pa-8 order-2 order-md-1">
          <h2 class="section-title animate__animated animate__fadeInLeft">
            Tailored Solutions
          </h2>
          <p
            class="section-subtitle animate__animated animate__fadeInLeft animate__delay-1s"
          >
            Every school is unique. We provide custom development to integrate
            with your systems or build specialized features to meet your needs.
          </p>
          <v-btn color="blue" large rounded href="#contact" class="section-btn">
            Request a Quote
          </v-btn>
        </v-col>
        <v-col cols="12" md="6" class="order-1 order-md-2">
          <v-img
            src="./assets/attendance.png"
            height="400"
            class="solutions-img animate__animated animate__fadeInRight"
          ></v-img>
        </v-col>
      </v-row>
    </v-container>

    <!-- Data Upload Section -->
    <v-container class="data-section">
      <v-row align="center">
        <v-col cols="12" md="6" order="2" order-md="1">
          <v-img
            src="https://images.unsplash.com/photo-1451187580459-43490279c0b5?ixlib=rb-4.0.3&auto=format&fit=crop&w=600&q=80"
            height="400"
            class="data-img animate__animated animate__fadeInLeft"
          ></v-img>
        </v-col>
        <v-col cols="12" md="6" class="pa-8" order="1" order-md="2">
          <h2 class="section-title animate__animated animate__fadeInRight">
            Effortless Data Integration
          </h2>
          <p
            class="section-subtitle animate__animated animate__fadeInRight animate__delay-1s"
          >
            Upload student records, schedules, and more with our secure,
            user-friendly platform. Get started in minutes.
          </p>
          <v-btn color="pink" large rounded class="section-btn">
            Explore Integration
          </v-btn>
        </v-col>
      </v-row>
    </v-container>

    <!-- Contact Form Section -->
    <v-container id="contact" fluid class="contact-section">
      <v-row>
        <v-col cols="12" class="text-center">
          <h2
            class="section-title text-white animate__animated animate__fadeInUp"
          >
            Let’s Connect
          </h2>
          <p
            class="section-subtitle text-white animate__animated animate__fadeInUp animate__delay-1s"
          >
            Reach out to schedule a demo or discuss your needs
          </p>
        </v-col>
      </v-row>
      <v-row justify="center">
        <v-col cols="12" md="6">
          <v-form v-model="valid" ref="form" class="contact-form">
            <v-text-field
              v-model="name"
              :rules="nameRules"
              label="Name"
              required
              dark
              filled
              rounded
              class="form-field"
            ></v-text-field>
            <v-text-field
              v-model="email"
              :rules="emailRules"
              label="Email"
              required
              dark
              filled
              rounded
              class="form-field"
            ></v-text-field>
            <v-textarea
              v-model="message"
              :rules="messageRules"
              label="Message"
              required
              dark
              filled
              rounded
              class="form-field"
            ></v-textarea>
            <v-btn
              color="pink"
              large
              rounded
              @click="submit"
              :disabled="!valid || loading"
              class="form-btn"
            >
              <v-progress-circular
                v-if="loading"
                indeterminate
                size="20"
                color="white"
                class="mr-2"
              ></v-progress-circular>
              Send Message
            </v-btn>
          </v-form>
        </v-col>
      </v-row>
    </v-container>

    <!-- Footer -->
    <v-footer class="footer">
      <v-row>
        <v-col cols="12" class="text-center">
          <p class="footer-text">© 2025 SchoolSync. All rights reserved.</p>
        </v-col>
      </v-row>
    </v-footer>
    <v-dialog v-model="dialog" max-width="800">
      <v-card>
        <v-img :src="selectedImage" height="500" cover></v-img>
      </v-card>
    </v-dialog>
  </v-app>
  <v-snackbar
    v-model="snackbar"
    :color="snackbarColor"
    timeout="4000"
    top
    right
  >
    {{ snackbarText }}
    <template v-slot:action="{ attrs }">
      <v-btn color="white" text v-bind="attrs" @click="snackbar = false">
        Close
      </v-btn>
    </template>
  </v-snackbar>
</template>

<script>
// import attendanceImg from "@/assets/attendance.png"; // adjust based on project structure
export default {
  data() {
    return {
      // ... your existing data ...
      drawer: false,
      valid: false, // you had true but v-form usually starts false
      name: "",
      email: "",
      message: "",
      nameRules: [(v) => !!v || "Name is required"],
      emailRules: [
        (v) => !!v || "Email is required",
        (v) => /.+@.+\..+/.test(v) || "Email must be valid",
      ],
      messageRules: [(v) => !!v || "Message is required"],
      features: [
        // your features...
      ],
      loading: false,
      snackbar: false,
      snackbarText: "",
      snackbarColor: "",
    };
  },
  methods: {
    async submit() {
      const form = this.$refs.form;
      if (!form.validate()) return;

      this.loading = true;
      this.snackbar = false;

      try {
        const response = await fetch(
          "https://10lgh1w6z8.execute-api.us-east-1.amazonaws.com/send-email",
          {
            method: "POST",
            headers: {
              "Content-Type": "application/json",
            },
            body: JSON.stringify({
              name: this.name,
              email: this.email,
              message: this.message,
            }),
          }
        );

        if (!response.ok) {
          throw new Error(`Server error: ${response.statusText}`);
        }

        const data = await response.json();

        if (data.error) {
          throw new Error(data.error);
        }

        this.snackbarText = "Message sent successfully!";
        this.snackbarColor = "success";
        this.snackbar = true;
        form.reset();
        this.valid = false; // reset form validity
      } catch (error) {
        this.snackbarText = `Failed to send message: ${error.message}`;
        this.snackbarColor = "error";
        this.snackbar = true;
      } finally {
        this.loading = false;
      }
    },

    openImage(img) {
      this.selectedImage = img;
      this.dialog = true;
    },
  },
};
</script>

<style scoped>
@import url("https://fonts.googleapis.com/css2?family=Inter:wght@300;400;600;700&display=swap");
@import url("https://cdnjs.cloudflare.com/ajax/libs/animate.css/4.1.1/animate.min.css");

* {
  font-family: "Inter", sans-serif;
  box-sizing: border-box;
}

html {
  scroll-behavior: smooth;
}

/* Hero Section */
.hero-parallax {
  position: relative;
}

.hero-overlay {
  position: absolute;
  inset: 0;
  background: linear-gradient(
    to right,
    rgba(30, 136, 229, 0.7),
    rgba(255, 64, 129, 0.7)
  );
  backdrop-filter: blur(5px);
}

.hero-content {
  position: relative;
  z-index: 10;
}

.hero-title {
  font-size: 4rem;
  font-weight: 700;
  color: white;
  margin-bottom: 1rem;
}

.hero-subtitle {
  font-size: 1.5rem;
  font-weight: 300;
  color: white;
  margin-bottom: 2rem;
}

.hero-btn {
  background-color: #ff4081 !important;
  color: white !important;
  padding: 0 2rem;
  font-size: 1.125rem;
  text-transform: capitalize;
  transition: background-color 0.3s ease;
}

.hero-btn:hover {
  background-color: #e91e63 !important;
}

@media (max-width: 600px) {
  .hero-title {
    font-size: 2.5rem;
  }
  .hero-subtitle {
    font-size: 1.25rem;
  }
}

/* Features Section */
.features-section {
  padding: 4rem 0;
  background-color: #f7fafc;
}

.section-title {
  font-size: 2.5rem;
  font-weight: 700;
  color: #1e88e5;
}

.section-subtitle {
  font-size: 1.25rem;
  font-weight: 300;
  color: #4a5568;
  margin-top: 1rem;
}

.features-grid {
  margin-top: 3rem;
}

.modern-card {
  background-color: white;
  border-radius: 1rem;
  transition: transform 0.3s ease, box-shadow 0.3s ease;
}

.modern-card:hover {
  transform: translateY(-5px);
  box-shadow: 0 20px 30px rgba(0, 0, 0, 0.15);
}

.feature-img {
  border-radius: 0.5rem;
}

.feature-title {
  font-size: 1.25rem;
  font-weight: 600;
  color: #1e88e5;
  margin-top: 1rem;
}

.feature-text {
  font-size: 1rem;
  color: #4a5568;
}

/* Solutions Section */
.solutions-section {
  padding: 4rem 0;
  background-color: #e3f2fd;
}

.solutions-img {
  border-radius: 1rem;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
}

.section-btn {
  background-color: #1e88e5 !important;
  color: white !important;
  font-size: 1.125rem;
  text-transform: capitalize;
  transition: background-color 0.3s ease;
}

.section-btn:hover {
  background-color: #1565c0 !important;
}

/* Data Section */
.data-section {
  padding: 4rem 0;
  background-color: #f7fafc;
}

.data-img {
  border-radius: 1rem;
  box-shadow: 0 10px 20px rgba(0, 0, 0, 0.1);
}

/* Contact Section */
.contact-section {
  padding: 4rem 0;
  background: linear-gradient(to right, #1e88e5, #ff4081);
}

.contact-form {
  background: rgba(255, 255, 255, 0.1);
}
</style>
