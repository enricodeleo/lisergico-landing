<template>
  <div class="lisergico-void">
    <!-- Floating consciousness orbs -->
    <div class="orb orb-1"></div>
    <div class="orb orb-2"></div>
    <div class="orb orb-3"></div>
    <div class="orb orb-4"></div>
    <div class="orb orb-5"></div>

    <!-- Morphing blob -->
    <div class="morph-blob"></div>

    <!-- Main content -->
    <main class="dream-container">
      <!-- Hero section -->
      <section class="hero-section">
        <div class="glitch-wrapper">
          <h1 class="title main-title" data-text="LISÉRGICO">
            <span class="title-letter" v-for="(char, i) in 'LISÉRGICO'" :style="{ '--i': i }">{{ char }}</span>
          </h1>
        </div>

        <p class="subtitle floating">
          <span class="wave-word">where</span>
          <span class="wave-word">dreams</span>
          <span class="wave-word">dissolve</span>
          <span class="wave-word">into</span>
          <span class="wave-word">infinity</span>
        </p>

        <div class="tagline-container">
          <p class="tagline">
            Born from 10 hours of synchronized dreaming, Lisergico is the digital manifestation
            of consciousness untethered. We exist at the intersection of kaleidoscope memories
            and electric sheep.
          </p>
        </div>

        <div class="cta-group">
          <button class="dream-btn primary">
            <span class="btn-text">Enter the Void</span>
            <span class="btn-glow"></span>
          </button>
          <button class="dream-btn secondary">
            <span class="btn-text">Summon Your Dreams</span>
          </button>
        </div>
      </section>

      <!-- Manifesto section -->
      <section class="manifesto-section">
        <div class="manifesto-grid">
          <div class="manifesto-card" v-for="(card, i) in manifestoCards" :key="i" :style="{ '--delay': i * 0.2 }">
            <div class="card-icon">{{ card.icon }}</div>
            <h3 class="card-title">{{ card.title }}</h3>
            <p class="card-text">{{ card.text }}</p>
          </div>
        </div>
      </section>

      <!-- Dream features -->
      <section class="features-section">
        <h2 class="section-title">
          <span class="title-word">The</span>
          <span class="title-word title-accent">Seven</span>
          <span class="title-word">Realms</span>
        </h2>

        <div class="realms-grid">
          <div class="realm" v-for="(realm, i) in realms" :key="i">
            <div class="realm-number">0{{ i + 1 }}</div>
            <h4 class="realm-name">{{ realm.name }}</h4>
            <p class="realm-desc">{{ realm.desc }}</p>
            <div class="realm-border"></div>
          </div>
        </div>
      </section>

      <!-- Floating quote -->
      <section class="quote-section">
        <blockquote class="dream-quote">
          "Reality is just a collective hallucination we all agreed to share.
          <span class="quote-break">Lisergico is the exception to that agreement.</span>"
        </blockquote>
        <cite class="quote-author">— The Dreamer Who Woke Up</cite>
      </section>

      <!-- Footer -->
      <footer class="void-footer">
        <div class="footer-void">
          <p class="footer-text">∞ Lisergico exists where seconds stretch into eternities ∞</p>
          <div class="footer-symbols">
            <span class="symbol">◈</span>
            <span class="symbol">❋</span>
            <span class="symbol">⧫</span>
            <span class="symbol">◈</span>
          </div>
        </div>
      </footer>
    </main>

    <!-- Grain overlay -->
    <div class="grain-overlay"></div>

    <!-- Scanlines -->
    <div class="scanlines"></div>
  </div>
</template>

<script setup>
const manifestoCards = [
  {
    icon: '◉',
    title: 'Consciousness Expansion',
    text: 'Your mind is a fractal. Each thought contains infinite thoughts. We help you navigate the recursion without losing yourself in the loop.'
  },
  {
    icon: '◎',
    title: 'Temporal Fluidity',
    text: 'Past, present, and future are merely suggestions. Our technology lets you experience moments sideways, backward, and in colors that don\'t have names yet.'
  },
  {
    icon: '◈',
    title: 'Sensory Synthesis',
    text: 'Taste sounds. See music. Hear thoughts. We dissolve the boundaries between your senses until perception itself becomes a collage of impossible beauty.'
  }
]

const realms = [
  { name: 'Prism Palace', desc: 'Where light becomes thought and colors have conversations with your memories' },
  { name: 'Echo Garden', desc: 'Every sound you\'ve ever heard grows here, crystallized into harmonic flowers' },
  { name: 'Mirror Maze', desc: 'Infinite reflections of yourself, each one slightly more honest than the last' },
  { name: 'Silicon Savannah', desc: 'Digital lions made of pure mathematics hunt for your deepest fears' },
  { name: 'Neon Nirvana', desc: 'The space between blinks, where electric monks meditate on the nature of voltage' },
  { name: 'Dream Embassy', desc: 'Diplomatic relations between your sleeping and waking selves are negotiated here' },
  { name: 'The Edge', desc: 'Standing at the boundary of understanding, looking into the beautiful void of not-knowing' }
]
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Creepster&family=Space+Mono:ital,wght@0,400;0,700;1,400&family=Abril+Fatface&display=swap');

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

:root {
  --electric-pink: #ff00ff;
  --cyan-dream: #00ffff;
  --acid-green: #39ff14;
  --deep-void: #0a001a;
  --neon-purple: #bf00ff;
  --sunset-orange: #ff6b35;
  --dream-blue: #4361ee;
  --plasma-yellow: #fff700;
}

.lisergico-void {
  min-height: 100vh;
  background: var(--deep-void);
  overflow-x: hidden;
  position: relative;
  font-family: 'Space Mono', monospace;
  color: #fff;
}

/* Floating orbs */
.orb {
  position: fixed;
  border-radius: 50%;
  filter: blur(80px);
  opacity: 0.6;
  pointer-events: none;
  z-index: 0;
  animation: float-orb 20s ease-in-out infinite;
}

.orb-1 {
  width: 600px;
  height: 600px;
  background: radial-gradient(circle, var(--neon-purple) 0%, transparent 70%);
  top: -200px;
  left: -200px;
  animation-delay: 0s;
}

.orb-2 {
  width: 500px;
  height: 500px;
  background: radial-gradient(circle, var(--cyan-dream) 0%, transparent 70%);
  top: 50%;
  right: -150px;
  animation-delay: -5s;
}

.orb-3 {
  width: 400px;
  height: 400px;
  background: radial-gradient(circle, var(--electric-pink) 0%, transparent 70%);
  bottom: -100px;
  left: 30%;
  animation-delay: -10s;
}

.orb-4 {
  width: 350px;
  height: 350px;
  background: radial-gradient(circle, var(--acid-green) 0%, transparent 70%);
  top: 40%;
  left: 10%;
  animation-delay: -15s;
}

.orb-5 {
  width: 450px;
  height: 450px;
  background: radial-gradient(circle, var(--sunset-orange) 0%, transparent 70%);
  bottom: 20%;
  right: 20%;
  animation-delay: -7s;
}

@keyframes float-orb {
  0%, 100% { transform: translate(0, 0) scale(1); }
  25% { transform: translate(50px, -50px) scale(1.1); }
  50% { transform: translate(-30px, 30px) scale(0.9); }
  75% { transform: translate(-50px, -30px) scale(1.05); }
}

/* Morphing blob */
.morph-blob {
  position: fixed;
  width: 800px;
  height: 800px;
  top: 50%;
  left: 50%;
  transform: translate(-50%, -50%);
  background: linear-gradient(45deg,
    var(--neon-purple) 0%,
    var(--electric-pink) 25%,
    var(--cyan-dream) 50%,
    var(--acid-green) 75%,
    var(--neon-purple) 100%);
  background-size: 400% 400%;
  border-radius: 60% 40% 30% 70% / 60% 30% 70% 40%;
  filter: blur(100px);
  opacity: 0.3;
  animation: morph 15s ease-in-out infinite, gradient-shift 10s ease infinite;
  pointer-events: none;
  z-index: 0;
}

@keyframes morph {
  0%, 100% { border-radius: 60% 40% 30% 70% / 60% 30% 70% 40%; }
  25% { border-radius: 30% 60% 70% 40% / 50% 60% 30% 60%; }
  50% { border-radius: 50% 60% 30% 60% / 30% 40% 70% 60%; }
  75% { border-radius: 60% 30% 60% 50% / 40% 70% 50% 30%; }
}

@keyframes gradient-shift {
  0%, 100% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
}

/* Main content */
.dream-container {
  position: relative;
  z-index: 1;
  padding: 0 2rem;
}

/* Hero section */
.hero-section {
  min-height: 100vh;
  display: flex;
  flex-direction: column;
  justify-content: center;
  align-items: center;
  text-align: center;
  padding: 4rem 0;
}

/* Glitch title */
.glitch-wrapper {
  perspective: 1000px;
}

.main-title {
  font-family: 'Abril Fatface', cursive;
  font-size: clamp(4rem, 20vw, 15rem);
  font-weight: 400;
  letter-spacing: 0.05em;
  background: linear-gradient(135deg,
    var(--electric-pink) 0%,
    var(--cyan-dream) 25%,
    var(--acid-green) 50%,
    var(--plasma-yellow) 75%,
    var(--electric-pink) 100%);
  background-size: 300% 300%;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  animation: gradient-flow 8s ease infinite;
  position: relative;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 0.1em;
}

.main-title::before,
.main-title::after {
  content: attr(data-text);
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: inherit;
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
}

.main-title::before {
  animation: glitch-1 0.3s infinite linear alternate-reverse;
  clip-path: polygon(0 0, 100% 0, 100% 35%, 0 35%);
}

.main-title::after {
  animation: glitch-2 0.3s infinite linear alternate-reverse;
  clip-path: polygon(0 65%, 100% 65%, 100% 100%, 0 100%);
}

@keyframes gradient-flow {
  0%, 100% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
}

@keyframes glitch-1 {
  0% { transform: translateX(0); }
  20% { transform: translateX(-3px); }
  40% { transform: translateX(3px); }
  60% { transform: translateX(-3px); }
  80% { transform: translateX(3px); }
  100% { transform: translateX(0); }
}

@keyframes glitch-2 {
  0% { transform: translateX(0); }
  20% { transform: translateX(3px); }
  40% { transform: translateX(-3px); }
  60% { transform: translateX(3px); }
  80% { transform: translateX(-3px); }
  100% { transform: translateX(0); }
}

.title-letter {
  display: inline-block;
  animation: letter-float 3s ease-in-out infinite;
  animation-delay: calc(var(--i) * 0.1s);
}

@keyframes letter-float {
  0%, 100% { transform: translateY(0) rotate(0deg); }
  50% { transform: translateY(-20px) rotate(3deg); }
}

/* Subtitle */
.subtitle {
  font-size: clamp(1.2rem, 4vw, 2rem);
  margin-top: 2rem;
  font-weight: 400;
  letter-spacing: 0.3em;
  text-transform: lowercase;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 0.5em 1em;
}

.wave-word {
  display: inline-block;
  animation: word-wave 2s ease-in-out infinite;
  animation-delay: calc(var(--i, 0) * 0.15s);
  color: var(--cyan-dream);
  text-shadow: 0 0 20px var(--cyan-dream), 0 0 40px var(--cyan-dream);
}

.wave-word:nth-child(2) {
  animation-delay: 0.2s;
  color: var(--electric-pink);
  text-shadow: 0 0 20px var(--electric-pink), 0 0 40px var(--electric-pink);
}

.wave-word:nth-child(3) {
  animation-delay: 0.4s;
  color: var(--acid-green);
  text-shadow: 0 0 20px var(--acid-green), 0 0 40px var(--acid-green);
}

.wave-word:nth-child(4) {
  animation-delay: 0.6s;
  color: var(--plasma-yellow);
  text-shadow: 0 0 20px var(--plasma-yellow), 0 0 40px var(--plasma-yellow);
}

.wave-word:nth-child(5) {
  animation-delay: 0.8s;
  color: var(--sunset-orange);
  text-shadow: 0 0 20px var(--sunset-orange), 0 0 40px var(--sunset-orange);
}

@keyframes word-wave {
  0%, 100% { transform: translateY(0) scale(1); }
  50% { transform: translateY(-10px) scale(1.05); }
}

.floating {
  animation: container-float 6s ease-in-out infinite;
}

@keyframes container-float {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-15px); }
}

/* Tagline */
.tagline-container {
  max-width: 600px;
  margin: 3rem auto;
  padding: 2rem;
  border: 1px solid rgba(255, 255, 255, 0.1);
  background: rgba(10, 0, 26, 0.5);
  backdrop-filter: blur(10px);
  border-radius: 20px;
  position: relative;
  overflow: hidden;
}

.tagline-container::before {
  content: '';
  position: absolute;
  top: -2px;
  left: -2px;
  right: -2px;
  bottom: -2px;
  background: linear-gradient(45deg,
    var(--electric-pink), var(--cyan-dream),
    var(--acid-green), var(--neon-purple));
  background-size: 400% 400%;
  animation: border-glow 6s ease infinite;
  border-radius: 22px;
  z-index: -1;
  opacity: 0.5;
}

@keyframes border-glow {
  0%, 100% { background-position: 0% 50%; }
  50% { background-position: 100% 50%; }
}

.tagline {
  font-size: 1rem;
  line-height: 1.8;
  color: rgba(255, 255, 255, 0.8);
  font-weight: 400;
}

/* CTA buttons */
.cta-group {
  display: flex;
  flex-wrap: wrap;
  gap: 1.5rem;
  justify-content: center;
  margin-top: 3rem;
}

.dream-btn {
  position: relative;
  padding: 1.2rem 2.5rem;
  font-family: 'Space Mono', monospace;
  font-size: 1rem;
  font-weight: 700;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  border: none;
  cursor: pointer;
  overflow: hidden;
  transition: all 0.3s ease;
}

.dream-btn.primary {
  background: linear-gradient(135deg, var(--neon-purple), var(--electric-pink));
  color: #fff;
  border-radius: 50px;
  box-shadow:
    0 0 30px rgba(255, 0, 255, 0.4),
    0 0 60px rgba(255, 0, 255, 0.2),
    inset 0 0 30px rgba(255, 255, 255, 0.1);
}

.dream-btn.primary:hover {
  transform: scale(1.05) translateY(-3px);
  box-shadow:
    0 0 50px rgba(255, 0, 255, 0.6),
    0 0 100px rgba(255, 0, 255, 0.4),
    inset 0 0 30px rgba(255, 255, 255, 0.2);
}

.dream-btn.secondary {
  background: transparent;
  color: var(--cyan-dream);
  border: 2px solid var(--cyan-dream);
  border-radius: 50px;
  box-shadow:
    0 0 20px rgba(0, 255, 255, 0.2),
    inset 0 0 20px rgba(0, 255, 255, 0.1);
}

.dream-btn.secondary:hover {
  background: rgba(0, 255, 255, 0.1);
  transform: scale(1.05) translateY(-3px);
  box-shadow:
    0 0 40px rgba(0, 255, 255, 0.4),
    inset 0 0 30px rgba(0, 255, 255, 0.2);
}

.btn-text {
  position: relative;
  z-index: 1;
}

/* Manifesto section */
.manifesto-section {
  padding: 8rem 0;
}

.manifesto-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
  gap: 2rem;
  max-width: 1200px;
  margin: 0 auto;
}

.manifesto-card {
  background: rgba(255, 255, 255, 0.03);
  backdrop-filter: blur(20px);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 30px;
  padding: 3rem 2rem;
  text-align: center;
  transition: all 0.5s cubic-bezier(0.23, 1, 0.32, 1);
  animation: card-emerge 1s ease forwards;
  animation-delay: var(--delay);
  opacity: 0;
  transform: translateY(50px);
}

@keyframes card-emerge {
  to {
    opacity: 1;
    transform: translateY(0);
  }
}

.manifesto-card:hover {
  transform: translateY(-10px) rotateX(5deg);
  background: rgba(255, 255, 255, 0.05);
  box-shadow:
    0 30px 60px rgba(0, 0, 0, 0.3),
    0 0 40px rgba(191, 0, 255, 0.2);
  border-color: rgba(191, 0, 255, 0.3);
}

.card-icon {
  font-size: 4rem;
  margin-bottom: 1.5rem;
  background: linear-gradient(135deg, var(--electric-pink), var(--cyan-dream));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  animation: icon-pulse 3s ease-in-out infinite;
}

@keyframes icon-pulse {
  0%, 100% { transform: scale(1); filter: drop-shadow(0 0 20px var(--electric-pink)); }
  50% { transform: scale(1.1); filter: drop-shadow(0 0 40px var(--cyan-dream)); }
}

.card-title {
  font-family: 'Abril Fatface', cursive;
  font-size: 1.8rem;
  margin-bottom: 1rem;
  color: #fff;
}

.card-text {
  font-size: 0.95rem;
  line-height: 1.7;
  color: rgba(255, 255, 255, 0.7);
}

/* Features section */
.features-section {
  padding: 8rem 0;
  text-align: center;
}

.section-title {
  font-family: 'Abril Fatface', cursive;
  font-size: clamp(2.5rem, 8vw, 6rem);
  margin-bottom: 4rem;
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  gap: 0.3em;
}

.title-word {
  color: #fff;
  animation: title-word 4s ease-in-out infinite;
}

.title-word:nth-child(1) { animation-delay: 0s; }
.title-word:nth-child(3) { animation-delay: 0.4s; }

@keyframes title-word {
  0%, 100% { transform: translateY(0); }
  50% { transform: translateY(-15px); }
}

.title-accent {
  background: linear-gradient(135deg, var(--acid-green), var(--cyan-dream));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  animation: title-accent 4s ease-in-out infinite, hue-shift 10s linear infinite;
}

@keyframes hue-shift {
  0%, 100% { filter: hue-rotate(0deg); }
  50% { filter: hue-rotate(180deg); }
}

.realms-grid {
  display: grid;
  grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
  gap: 1.5rem;
  max-width: 1400px;
  margin: 0 auto;
}

.realm {
  position: relative;
  background: rgba(10, 0, 26, 0.6);
  backdrop-filter: blur(10px);
  border: 1px solid rgba(255, 255, 255, 0.08);
  border-radius: 20px;
  padding: 2rem;
  text-align: left;
  overflow: hidden;
  transition: all 0.4s ease;
}

.realm::before {
  content: '';
  position: absolute;
  top: 0;
  left: 0;
  right: 0;
  height: 3px;
  background: linear-gradient(90deg,
    var(--neon-purple), var(--electric-pink),
    var(--cyan-dream), var(--acid-green));
  background-size: 300% 100%;
  animation: gradient-flow 4s ease infinite;
}

.realm:hover {
  transform: translateY(-5px) scale(1.02);
  border-color: rgba(191, 0, 255, 0.3);
  box-shadow:
    0 20px 40px rgba(0, 0, 0, 0.3),
    0 0 30px rgba(191, 0, 255, 0.15);
}

.realm-number {
  font-family: 'Abril Fatface', cursive;
  font-size: 3rem;
  background: linear-gradient(135deg, var(--electric-pink), var(--neon-purple));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  opacity: 0.5;
  margin-bottom: 0.5rem;
}

.realm-name {
  font-family: 'Abril Fatface', cursive;
  font-size: 1.5rem;
  color: #fff;
  margin-bottom: 0.8rem;
}

.realm-desc {
  font-size: 0.9rem;
  line-height: 1.6;
  color: rgba(255, 255, 255, 0.6);
}

.realm-border {
  position: absolute;
  bottom: 0;
  right: 0;
  width: 50px;
  height: 50px;
  border-bottom: 2px solid var(--cyan-dream);
  border-right: 2px solid var(--cyan-dream);
  border-radius: 0 0 20px 0;
  opacity: 0.5;
}

/* Quote section */
.quote-section {
  padding: 10rem 2rem;
  text-align: center;
  position: relative;
}

.dream-quote {
  font-family: 'Abril Fatface', cursive;
  font-size: clamp(1.5rem, 4vw, 3rem);
  line-height: 1.4;
  max-width: 900px;
  margin: 0 auto 2rem;
  color: #fff;
  position: relative;
}

.dream-quote::before,
.dream-quote::after {
  content: '"';
  font-size: 6rem;
  position: absolute;
  color: var(--electric-pink);
  opacity: 0.3;
  font-family: 'Creepster', cursive;
}

.dream-quote::before {
  top: -2rem;
  left: -2rem;
}

.dream-quote::after {
  bottom: -4rem;
  right: -2rem;
}

.quote-break {
  display: block;
  color: var(--cyan-dream);
  text-shadow: 0 0 30px var(--cyan-dream);
}

.quote-author {
  font-size: 1rem;
  color: rgba(255, 255, 255, 0.5);
  font-style: normal;
  letter-spacing: 0.2em;
  text-transform: uppercase;
}

/* Footer */
.void-footer {
  padding: 4rem 2rem;
  text-align: center;
  border-top: 1px solid rgba(255, 255, 255, 0.05);
}

.footer-text {
  font-size: 0.9rem;
  color: rgba(255, 255, 255, 0.4);
  margin-bottom: 1.5rem;
  letter-spacing: 0.1em;
}

.footer-symbols {
  display: flex;
  justify-content: center;
  gap: 2rem;
}

.symbol {
  font-size: 1.5rem;
  color: var(--neon-purple);
  animation: symbol-float 3s ease-in-out infinite;
}

.symbol:nth-child(1) { animation-delay: 0s; }
.symbol:nth-child(2) { animation-delay: 0.5s; }
.symbol:nth-child(3) { animation-delay: 1s; }
.symbol:nth-child(4) { animation-delay: 1.5s; }

@keyframes symbol-float {
  0%, 100% {
    transform: translateY(0);
    text-shadow: 0 0 10px var(--neon-purple);
  }
  50% {
    transform: translateY(-10px);
    text-shadow: 0 0 30px var(--neon-purple), 0 0 50px var(--electric-pink);
  }
}

/* Grain overlay */
.grain-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 100;
  opacity: 0.05;
  background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)'/%3E%3C/svg%3E");
}

/* Scanlines */
.scanlines {
  position: fixed;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  pointer-events: none;
  z-index: 99;
  background: repeating-linear-gradient(
    0deg,
    rgba(0, 0, 0, 0.1) 0px,
    rgba(0, 0, 0, 0.1) 1px,
    transparent 1px,
    transparent 3px
  );
  opacity: 0.3;
}

/* Responsive */
@media (max-width: 768px) {
  .cta-group {
    flex-direction: column;
    align-items: center;
  }

  .dream-btn {
    width: 100%;
    max-width: 300px;
  }

  .dream-quote::before,
  .dream-quote::after {
    font-size: 3rem;
  }

  .dream-quote::before {
    top: -1rem;
    left: 0;
  }

  .dream-quote::after {
    bottom: -2rem;
    right: 0;
  }
}

/* Custom scrollbar */
::-webkit-scrollbar {
  width: 8px;
}

::-webkit-scrollbar-track {
  background: var(--deep-void);
}

::-webkit-scrollbar-thumb {
  background: linear-gradient(var(--neon-purple), var(--electric-pink));
  border-radius: 4px;
}
</style>
