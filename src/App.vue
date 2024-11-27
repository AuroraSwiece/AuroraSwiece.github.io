<template>
  <div id="app" class="landing-page">
    <header class="header">
      <h1 class="title">Premium Crystal Candle</h1>
      <p class="subtitle">
        Experience elegance and sophistication with our luxurious candle centerpiece. Designed for connoisseurs of style, it transforms any space into an oasis of calm and beauty.
      </p>
    </header>

    <main class="main-content">
      <div class="product-showcase">
        <!-- Placeholder for Product Image -->
        <img
          src="https://via.placeholder.com/400x300"
          alt="Large crystal bowl with premium wax on a metal stand"
          class="product-image"
        />
        <p class="product-description">
          The centerpiece features a large crystal bowl, hand-crafted for brilliance, filled with high-quality wax for a radiant, long-lasting flame. Supported by a stable and elegant steel rod structure, it offers unmatched durability and style.
        </p>
      </div>

      <div class="contact-form">
        <h2>Get More Information</h2>
        <p>Leave your email or phone number, and we'll contact you with all the details.</p>
        <form @submit.prevent="submitContact">
          <input
            type="email"
            v-model="email"
            placeholder="Your Email"
            required
          />
          <p class="or-divider">or</p>
          <input
            type="tel"
            v-model="phone"
            placeholder="Your Phone Number"
            required
          />
          <button type="submit">Submit</button>
        </form>
        <p class="success-message" v-if="successMessage">{{ successMessage }}</p>
      </div>
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
.landing-page {
  font-family: Arial, sans-serif;
  color: #333;
  text-align: center;
  margin: 0 auto;
  padding: 20px;
}

.header {
  margin-bottom: 30px;
}

.title {
  font-size: 2.5em;
  color: #5a5a5a;
}

.subtitle {
  font-size: 1.2em;
  color: #777;
}

.main-content {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.product-showcase {
  margin-bottom: 30px;
}

.product-image {
  max-width: 100%;
  border: 1px solid #ddd;
  border-radius: 10px;
}

.product-description {
  margin-top: 15px;
  font-size: 1em;
  color: #555;
}

.contact-form {
  background: #f9f9f9;
  padding: 20px;
  border-radius: 10px;
  width: 100%;
  max-width: 400px;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
}

.contact-form h2 {
  margin-bottom: 10px;
  color: #444;
}

.contact-form p {
  margin: 10px 0;
  font-size: 0.9em;
  color: #666;
}

.contact-form input {
  width: 100%;
  padding: 10px;
  margin: 5px 0;
  font-size: 1em;
  border: 1px solid #ccc;
  border-radius: 5px;
}

.contact-form .or-divider {
  margin: 10px 0;
  font-style: italic;
  color: #888;
}

.contact-form button {
  width: 100%;
  padding: 10px;
  font-size: 1em;
  background-color: #5a5a5a;
  color: #fff;
  border: none;
  border-radius: 5px;
  cursor: pointer;
}

.contact-form button:hover {
  background-color: #444;
}

.success-message {
  margin-top: 15px;
  color: green;
}
</style>
