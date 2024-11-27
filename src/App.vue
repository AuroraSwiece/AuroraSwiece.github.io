<template>
  <div id="app" class="landing-page">
    <header class="header">
      <h1 class="title">The Ultimate Premium Candle Experience</h1>
      <p class="subtitle">
        Transform your space with our meticulously crafted candle centerpiece. A fusion of elegance and functionality, designed to captivate and inspire.
      </p>
    </header>

    <main class="main-content">
      <section class="product-section">
        <div class="product-image-container">
          <img
            src="https://via.placeholder.com/500x400"
            alt="Premium crystal candle on a steel stand"
            class="product-image"
          />
        </div>
        <div class="product-details">
          <h2>About the Candle</h2>
          <p>
            This exquisite piece combines modern design with timeless charm. A crystal-clear bowl, filled with richly textured premium wax, rests atop a hand-crafted steel frame. Standing at an impressive height of 1 meter, it adds a luxurious touch to any space.
          </p>
          <p>
            Perfect for creating an ambiance of warmth and sophistication, this candle is a centerpiece that speaks volumes about your refined taste.
          </p>
        </div>
      </section>

      <section class="contact-form-section">
        <h2>Interested? Get in Touch</h2>
        <p>
          Share your email or phone number, and we’ll provide you with all the details about this one-of-a-kind creation.
        </p>
        <form @submit.prevent="submitContact" class="contact-form">
          <input
            type="email"
            v-model="email"
            placeholder="Enter your email"
            required
            class="form-input"
          />
          <p class="or-divider">or</p>
          <input
            type="tel"
            v-model="phone"
            placeholder="Enter your phone number"
            required
            class="form-input"
          />
          <button type="submit" class="submit-button">Submit</button>
        </form>
        <p class="success-message" v-if="successMessage">{{ successMessage }}</p>
      </section>
    </main>
  </div>
</template>

<script>
export default {
  data() {
    return {
      email: "",
      phone: "",
      successMessage: "",
    };
  },
  methods: {
    async submitContact() {
      try {
        const response = await fetch("http://localhost:8080/my/api", {
          method: "POST",
          headers: { "Content-Type": "application/json" },
          body: JSON.stringify({ email: this.email, phone: this.phone }),
        });

        if (response.ok) {
          this.successMessage = "Thank you! We'll get in touch soon.";
          this.email = "";
          this.phone = "";
        } else {
          this.successMessage = "Something went wrong. Please try again.";
        }
      } catch (error) {
        this.successMessage = "Error: Unable to submit your information.";
      }
    },
  },
};
</script>

<style>
/* General Styling */
body {
  margin: 0;
  font-family: "Merriweather", serif;
  color: #333;
  background: linear-gradient(120deg, #ffffff, #f0f4f8);
}

.landing-page {
  max-width: 1200px;
  margin: 0 auto;
  padding: 20px;
  text-align: center;
}

/* Header */
.header {
  margin-bottom: 40px;
}

.title {
  font-size: 3em;
  font-weight: bold;
  color: #2c3e50;
}

.subtitle {
  font-size: 1.2em;
  color: #7f8c8d;
  max-width: 700px;
  margin: 0 auto;
}

/* Main Content */
.main-content {
  display: flex;
  flex-direction: column;
  gap: 40px;
}

/* Product Section */
.product-section {
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  justify-content: center;
  gap: 30px;
  padding: 20px;
  background: #fdfdfd;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  border-radius: 10px;
}

.product-image-container {
  flex: 1;
  text-align: center;
}

.product-image {
  max-width: 100%;
  border-radius: 10px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.2);
}

.product-details {
  flex: 1;
  text-align: left;
  max-width: 600px;
}

.product-details h2 {
  font-size: 2em;
  color: #2c3e50;
  margin-bottom: 15px;
}

.product-details p {
  font-size: 1.1em;
  color: #555;
  line-height: 1.6;
}

/* Contact Form Section */
.contact-form-section {
  padding: 20px;
  background: #eaf2f8;
  border-radius: 10px;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
}

.contact-form-section h2 {
  font-size: 2em;
  color: #2c3e50;
}

.contact-form-section p {
  font-size: 1em;
  color: #7f8c8d;
  margin-bottom: 20px;
}

.contact-form {
  display: flex;
  flex-direction: column;
  gap: 15px;
  max-width: 400px;
  margin: 0 auto;
}

.form-input {
  padding: 10px;
  font-size: 1em;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.or-divider {
  font-size: 0.9em;
  color: #555;
}

.submit-button {
  padding: 10px 20px;
  font-size: 1.2em;
  background-color: #2c3e50;
  color: white;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  transition: background-color 0.3s ease;
}

.submit-button:hover {
  background-color: #34495e;
}

.success-message {
  margin-top: 15px;
  font-size: 1em;
  color: green;
}
</style>
