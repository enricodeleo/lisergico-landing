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
          <button class="dream-btn primary" @click="enterTheVoid">
            <span class="btn-text">Enter the Void</span>
            <span class="btn-glow"></span>
          </button>
          <button class="dream-btn secondary" @click="summonDreams">
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

    <!-- Void Overlay -->
    <Transition name="void">
      <div v-if="voidActive" class="void-overlay" @click="exitVoid">
        <div class="void-content">
          <div class="void-tunnel" v-for="i in 12" :key="i" :style="{ '--i': i }"></div>
          <div class="void-particles">
            <div v-for="i in 50" :key="i" class="particle" :style="particleStyle(i)"></div>
          </div>
          <div class="void-text">
            <h2 class="void-message">{{ voidMessage }}</h2>
          </div>
        </div>
        <button class="void-close" @click="exitVoid">
          <span>return to reality</span>
        </button>
      </div>
    </Transition>

    <!-- Dream Summon Modal -->
    <Transition name="modal">
      <div v-if="dreamModalOpen" class="dream-modal-overlay" @click.self="closeDreamModal">
        <div class="dream-modal">
          <button class="modal-close" @click="closeDreamModal">×</button>

          <!-- Dream idea display -->
          <div v-if="!showForm" class="dream-idea-container">
            <div class="dream-icon">◈</div>
            <h3 class="dream-idea-title">The Void Whispered:</h3>
            <div class="dream-idea-card">
              <h4 class="idea-name">{{ currentDream.name }}</h4>
              <p class="idea-tagline">{{ currentDream.tagline }}</p>
              <p class="idea-description">{{ currentDream.description }}</p>
              <div class="idea-tags">
                <span v-for="tag in currentDream.tags" :key="tag" class="tag">{{ tag }}</span>
              </div>
            </div>
            <p class="dream-prompt">What's your dream?</p>
            <button class="dream-btn primary" @click="showForm = true">
              <span class="btn-text">Tell Us Your Vision</span>
            </button>
            <button class="dream-again-btn" @click="getRandomDream">
              <span>Summon Another</span>
            </button>
          </div>

          <!-- Lead gen form -->
          <div v-else class="dream-form-container">
            <h3 class="form-title">Plant Your Dream Seed</h3>
            <p class="form-subtitle">The collective consciousness is listening</p>

            <form @submit.prevent="submitDream" class="dream-form">
              <div class="form-group">
                <label for="name">Your Name</label>
                <input
                  id="name"
                  v-model="form.name"
                  type="text"
                  placeholder="Who are you, dreamer?"
                  required
                />
              </div>

              <div class="form-group">
                <label for="email">Email</label>
                <input
                  id="email"
                  v-model="form.email"
                  type="email"
                  placeholder="Where should we reach you?"
                  required
                />
              </div>

              <div class="form-group">
                <label for="phone">Phone</label>
                <input
                  id="phone"
                  v-model="form.phone"
                  type="tel"
                  placeholder="For urgent transcendence"
                />
              </div>

              <div class="form-group">
                <label for="description">Your Dream</label>
                <textarea
                  id="description"
                  v-model="form.description"
                  placeholder="Describe your vision... What keeps you awake at night?"
                  rows="4"
                  required
                ></textarea>
              </div>

              <div v-if="formStatus.message" :class="['form-status', formStatus.type]">
                {{ formStatus.message }}
              </div>

              <button type="submit" class="dream-btn primary full-width" :disabled="formStatus.loading">
                <span class="btn-text">{{ formStatus.loading ? 'Transmitting...' : 'Release Into the Void' }}</span>
              </button>
            </form>

            <button class="back-to-idea" @click="showForm = false">
              ← Back to the dream
            </button>
          </div>
        </div>
      </div>
    </Transition>

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

const startupDreams = [
  {
    name: 'NeuroBloom',
    tagline: 'AI-powered emotional gardens that grow from your thoughts',
    description: 'Imagine a digital sanctuary where your emotions become living flora. Using EEG headsets and biometric feedback, NeuroBloom visualizes your mental state as a thriving ecosystem. Anxious thoughts become resilient bamboo, joy manifests as cherry blossoms. Share your garden with others or keep it as a private meditation space.'
  },
  {
    name: 'TimeSwap',
    tagline: 'Peer-to-peer marketplace for trading life hours',
    description: 'A revolutionary platform where people exchange skills and services measured in time, not money. A retired carpenter in Osaka teaches woodworking to a Silicon Valley coder for 3 hours. In exchange, the coder debugs the carpenter\'s grandson\'s startup for 3 hours. No currency. Just pure human time, valued equally.'
  },
  {
    name: 'DreamWeaver VR',
    tagline: 'Shared lucid dreaming spaces for collaborative creativity',
    description: 'Sleep-based collaboration platform. Teams enter synchronized REM states where they can brainstorm, prototype, and create in a world limited only by imagination. Our patent-pending neural synchronization technology enables shared dreamscapes where the laws of physics are merely suggestions.'
  },
  {
    name: 'Mothbox',
    tagline: 'Social network that deletes everything after 24 hours',
    description: 'Anti-archival social media designed for authentic connection. Every post, message, and memory fragment permanently dissolves at sunrise. No history. No permanent record. Just ephemeral moments meant to be experienced, not collected. Be your true self when nothing lasts.'
  },
  {
    name: 'Symbiont',
    tagline: 'Wearable AI that learns to predict your needs before you conscious of them',
    description: 'A thin biosensor patch that learns your patterns so deeply it can act as your external consciousness. It orders groceries before you realize you\'re out. It suggests routes based on your mood, not just traffic. It\'s not an assistant—it\'s an extension of you, powered by swarm intelligence algorithms.'
  },
  {
    name: 'EchoLocation',
    tagline: 'AR audio tours narrated by people who loved these places',
    description: 'Augmented reality app where you hear the emotional history of spaces through recordings left by those who experienced them there. A bench where someone got engaged. A corner where a musician found inspiration. The world becomes a tapestry of human emotion, layered invisibly over physical reality.'
  },
  {
    name: 'Pulse',
    tagline: 'Dating app using only biosignals—no profiles, no photos, no chat',
    description: 'Match based on physiological compatibility. Wearables measure your response to curated experiences—music, art, stories. When two people\'s patterns synchronize, they\'re notified. No swiping, no carefully curated personas. Just bodies that resonate on the same frequency.'
  },
  {
    name: 'Museum of Lost Futures',
    tagline: 'VR experiences of futures that almost happened but didn\'t',
    description: 'An immersive journey through alternate timelines. The 1990s where the Soviet Union transitioned to democracy. The world where electric cars won in 1900. The timeline where we solved climate change in the 1980s. History museums show what was. We show what could have been.'
  },
  {
    name: 'SynthSkin',
    tagline: ' programmable smart tattoos that change with your mood',
    description: 'E-ink tattoos embedded in a thin second skin. Display your current mood, show notifications, or display art that evolves throughout the day. Fully programmable via app, completely reversible, and surprisingly beautiful. Your body as a canvas for living art.'
  },
  {
    name: 'Quiet',
    tagline: 'Silence-as-a-service: physical spaces guaranteed free of all electromagnetic signals',
    description: 'A network of faraday-shielded sanctuaries in every major city. Membership grants access to spaces completely free of Wi-Fi, cellular, and all electromagnetic radiation. The first luxury amenity of the 21st century isn\'t gold—it\'s genuine, complete disconnection from the digital world.'
  },
  {
    name: 'AncestorAI',
    tagline: 'Chat with your deceased relatives, trained on their voice and memories',
    description: 'Using voice recordings, messages, and photos, we create gentle AI approximations of lost loved ones. Not a replacement, but a bridge. Ask the questions you never got to ask. Hear familiar laughter one more time. Grief meets technology in a space of healing.'
  },
  {
    name: 'FoodPrint',
    tagline: 'Trace every ingredient back to the specific farm and farmer',
    description: 'Scan any meal and see the complete journey of every ingredient. The tomato in your salsa was grown by Maria\'s farm in California. The salt came from these specific ponds in Portugal. Connect with the humans who feed you. Know the story behind every bite.'
  }
]

// Void overlay state
const voidActive = ref(false)
const voidMessage = ref('ENTERING THE VOID...')
const voidMessages = [
  'ENTERING THE VOID...',
  'REALITY DISSOLVING...',
  'CONSCIOUSNESS EXPANDING...',
  'INFINITE POSSIBILITIES...',
  'YOU ARE THE UNIVERSE...',
  'THE UNIVERSE IS YOU...',
]

// Dream modal state
const dreamModalOpen = ref(false)
const currentDream = ref({})
const showForm = ref(false)

// Form state
const form = ref({
  name: '',
  email: '',
  phone: '',
  description: ''
})

const formStatus = ref({
  loading: false,
  message: '',
  type: ''
})

// Void functions
function enterTheVoid() {
  voidActive.value = true
  let i = 0
  const interval = setInterval(() => {
    i = (i + 1) % voidMessages.length
    voidMessage.value = voidMessages[i]
  }, 2000)

  // Store interval ID for cleanup
  voidMessage.value._interval = interval
}

function exitVoid() {
  voidActive.value = true
  voidMessage.value = 'RETURNING...'
  clearInterval(voidMessage.value._interval)

  setTimeout(() => {
    voidActive.value = false
  }, 500)
}

// Dream modal functions
function summonDreams() {
  getRandomDream()
  showForm.value = false
  dreamModalOpen.value = true
}

function getRandomDream() {
  currentDream.value = startupDreams[Math.floor(Math.random() * startupDreams.length)]
}

function closeDreamModal() {
  dreamModalOpen.value = false
  showForm.value = false
  formStatus.value = { loading: false, message: '', type: '' }
}

// Form submission
async function submitDream() {
  formStatus.value = { loading: true, message: '', type: '' }

  try {
    const response = await fetch('https://n8n.enricodeleo.com/webhook/lisergico-home', {
      method: 'POST',
      headers: {
        'Content-Type': 'application/json',
      },
      body: JSON.stringify({
        name: form.value.name,
        email: form.value.email,
        phone: form.value.phone,
        description: form.value.description,
        inspired_by: currentDream.value.name
      })
    })

    if (response.ok) {
      formStatus.value = {
        loading: false,
        message: '✧ Your dream has been released into the void. The collective consciousness will respond. ✧',
        type: 'success'
      }
      // Reset form after delay
      setTimeout(() => {
        form.value = { name: '', email: '', phone: '', description: '' }
        formStatus.value = { loading: false, message: '', type: '' }
        closeDreamModal()
      }, 3000)
    } else {
      throw new Error('Transmission failed')
    }
  } catch (error) {
    formStatus.value = {
      loading: false,
      message: 'The void is temporarily disturbed. Try again.',
      type: 'error'
    }
  }
}

// Particle style generator for void
function particleStyle(i) {
  return {
    '--x': Math.random() * 100,
    '--y': Math.random() * 100,
    '--delay': Math.random() * 2,
    '--size': Math.random() * 4 + 2
  }
}

// Initialize with a random dream
getRandomDream()
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

.dream-btn:disabled {
  opacity: 0.6;
  cursor: not-allowed;
}

.dream-btn.full-width {
  width: 100%;
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

/* Void Overlay */
.void-overlay {
  position: fixed;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background: #000;
  z-index: 1000;
  display: flex;
  flex-direction: column;
  align-items: center;
  justify-content: center;
  overflow: hidden;
}

.void-content {
  position: absolute;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
}

.void-tunnel {
  position: absolute;
  width: 100%;
  height: 100%;
  border-radius: 50%;
  border: 2px solid;
  animation: void-tunnel-spin 4s linear infinite;
  opacity: 0.5;
}

.void-tunnel:nth-child(1) { border-color: var(--electric-pink); animation-duration: 8s; }
.void-tunnel:nth-child(2) { border-color: var(--cyan-dream); animation-duration: 10s; animation-direction: reverse; }
.void-tunnel:nth-child(3) { border-color: var(--acid-green); animation-duration: 12s; }
.void-tunnel:nth-child(4) { border-color: var(--neon-purple); animation-duration: 6s; animation-direction: reverse; }
.void-tunnel:nth-child(5) { border-color: var(--sunset-orange); animation-duration: 9s; }
.void-tunnel:nth-child(6) { border-color: var(--plasma-yellow); animation-duration: 11s; animation-direction: reverse; }

@keyframes void-tunnel-spin {
  from { transform: rotate(0deg) scale(calc(1 - var(--i) * 0.05)); }
  to { transform: rotate(360deg) scale(calc(1 - var(--i) * 0.05)); }
}

.void-particles {
  position: absolute;
  inset: 0;
}

.particle {
  position: absolute;
  width: calc(var(--size) * 1px);
  height: calc(var(--size) * 1px);
  background: white;
  border-radius: 50%;
  left: calc(var(--x) * 1%);
  top: calc(var(--y) * 1%);
  animation: particle-fly 3s ease-in-out infinite;
  animation-delay: var(--delay);
}

@keyframes particle-fly {
  0%, 100% {
    transform: translate(0, 0) scale(1);
    opacity: 0;
  }
  50% {
    transform: translate(calc((var(--x) - 50) * 5px), calc((var(--y) - 50) * 5px)) scale(2);
    opacity: 1;
  }
}

.void-text {
  z-index: 1;
  text-align: center;
}

.void-message {
  font-family: 'Abril Fatface', cursive;
  font-size: clamp(2rem, 8vw, 6rem);
  color: #fff;
  text-shadow:
    0 0 20px var(--electric-pink),
    0 0 40px var(--cyan-dream),
    0 0 60px var(--acid-green);
  animation: void-pulse 1s ease-in-out infinite;
}

@keyframes void-pulse {
  0%, 100% {
    transform: scale(1);
    filter: hue-rotate(0deg);
  }
  50% {
    transform: scale(1.05);
    filter: hue-rotate(30deg);
  }
}

.void-close {
  position: absolute;
  bottom: 3rem;
  padding: 1rem 2rem;
  background: transparent;
  border: 2px solid rgba(255, 255, 255, 0.3);
  border-radius: 50px;
  color: #fff;
  font-family: 'Space Mono', monospace;
  font-size: 0.9rem;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  cursor: pointer;
  transition: all 0.3s ease;
  z-index: 10;
}

.void-close:hover {
  background: rgba(255, 255, 255, 0.1);
  border-color: #fff;
}

/* Void transition */
.void-enter-active,
.void-leave-active {
  transition: all 0.5s ease;
}

.void-enter-from,
.void-leave-to {
  opacity: 0;
}

.void-enter-from .void-tunnel,
.void-leave-to .void-tunnel {
  transform: scale(0);
}

/* Dream Modal */
.dream-modal-overlay {
  position: fixed;
  inset: 0;
  background: rgba(10, 0, 26, 0.9);
  backdrop-filter: blur(20px);
  z-index: 999;
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 2rem;
  overflow-y: auto;
}

.dream-modal {
  position: relative;
  max-width: 600px;
  width: 100%;
  background: rgba(20, 0, 40, 0.95);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 30px;
  padding: 3rem 2rem;
  animation: modal-emerge 0.5s cubic-bezier(0.23, 1, 0.32, 1);
}

@keyframes modal-emerge {
  from {
    opacity: 0;
    transform: scale(0.9) translateY(20px);
  }
  to {
    opacity: 1;
    transform: scale(1) translateY(0);
  }
}

.modal-close {
  position: absolute;
  top: 1.5rem;
  right: 1.5rem;
  width: 40px;
  height: 40px;
  background: transparent;
  border: none;
  color: rgba(255, 255, 255, 0.5);
  font-size: 2rem;
  line-height: 1;
  cursor: pointer;
  transition: all 0.3s ease;
}

.modal-close:hover {
  color: #fff;
  transform: rotate(90deg);
}

/* Dream Idea Display */
.dream-idea-container {
  text-align: center;
}

.dream-icon {
  font-size: 4rem;
  margin-bottom: 1rem;
  animation: icon-pulse 3s ease-in-out infinite;
}

.dream-idea-title {
  font-family: 'Space Mono', monospace;
  font-size: 0.9rem;
  text-transform: uppercase;
  letter-spacing: 0.2em;
  color: rgba(255, 255, 255, 0.5);
  margin-bottom: 1.5rem;
}

.dream-idea-card {
  background: rgba(255, 255, 255, 0.03);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 20px;
  padding: 2rem;
  margin-bottom: 2rem;
  position: relative;
  overflow: hidden;
}

.dream-idea-card::before {
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

.idea-name {
  font-family: 'Abril Fatface', cursive;
  font-size: 2rem;
  background: linear-gradient(135deg, var(--electric-pink), var(--cyan-dream));
  -webkit-background-clip: text;
  -webkit-text-fill-color: transparent;
  background-clip: text;
  margin-bottom: 0.5rem;
}

.idea-tagline {
  font-style: italic;
  color: rgba(255, 255, 255, 0.7);
  margin-bottom: 1rem;
}

.idea-description {
  line-height: 1.7;
  color: rgba(255, 255, 255, 0.8);
  margin-bottom: 1rem;
}

.idea-tags {
  display: flex;
  flex-wrap: wrap;
  gap: 0.5rem;
  justify-content: center;
}

.tag {
  padding: 0.3rem 0.8rem;
  background: rgba(191, 0, 255, 0.2);
  border: 1px solid rgba(191, 0, 255, 0.3);
  border-radius: 20px;
  font-size: 0.75rem;
  color: var(--cyan-dream);
}

.dream-prompt {
  font-family: 'Abril Fatface', cursive;
  font-size: 1.5rem;
  margin-bottom: 1.5rem;
  color: #fff;
}

.dream-again-btn {
  margin-top: 1rem;
  padding: 0.8rem 1.5rem;
  background: transparent;
  border: 1px solid rgba(255, 255, 255, 0.2);
  border-radius: 50px;
  color: rgba(255, 255, 255, 0.6);
  font-family: 'Space Mono', monospace;
  font-size: 0.85rem;
  cursor: pointer;
  transition: all 0.3s ease;
}

.dream-again-btn:hover {
  border-color: var(--cyan-dream);
  color: var(--cyan-dream);
}

/* Dream Form */
.dream-form-container {
  text-align: center;
}

.form-title {
  font-family: 'Abril Fatface', cursive;
  font-size: 2rem;
  margin-bottom: 0.5rem;
  color: #fff;
}

.form-subtitle {
  color: rgba(255, 255, 255, 0.5);
  margin-bottom: 2rem;
}

.dream-form {
  text-align: left;
}

.form-group {
  margin-bottom: 1.5rem;
}

.form-group label {
  display: block;
  font-family: 'Space Mono', monospace;
  font-size: 0.8rem;
  text-transform: uppercase;
  letter-spacing: 0.1em;
  color: rgba(255, 255, 255, 0.6);
  margin-bottom: 0.5rem;
}

.form-group input,
.form-group textarea {
  width: 100%;
  padding: 1rem 1.2rem;
  background: rgba(255, 255, 255, 0.05);
  border: 1px solid rgba(255, 255, 255, 0.1);
  border-radius: 12px;
  color: #fff;
  font-family: 'Space Mono', monospace;
  font-size: 0.95rem;
  transition: all 0.3s ease;
}

.form-group input:focus,
.form-group textarea:focus {
  outline: none;
  border-color: var(--cyan-dream);
  background: rgba(255, 255, 255, 0.08);
  box-shadow: 0 0 20px rgba(0, 255, 255, 0.1);
}

.form-group input::placeholder,
.form-group textarea::placeholder {
  color: rgba(255, 255, 255, 0.3);
}

.form-group textarea {
  resize: vertical;
  min-height: 100px;
}

.form-status {
  padding: 1rem;
  border-radius: 12px;
  margin-bottom: 1rem;
  font-size: 0.9rem;
  text-align: center;
}

.form-status.success {
  background: rgba(57, 255, 20, 0.1);
  border: 1px solid rgba(57, 255, 20, 0.3);
  color: var(--acid-green);
}

.form-status.error {
  background: rgba(255, 0, 255, 0.1);
  border: 1px solid rgba(255, 0, 255, 0.3);
  color: var(--electric-pink);
}

.back-to-idea {
  margin-top: 1rem;
  padding: 0.8rem 1.5rem;
  background: transparent;
  border: none;
  color: rgba(255, 255, 255, 0.5);
  font-family: 'Space Mono', monospace;
  font-size: 0.85rem;
  cursor: pointer;
  transition: all 0.3s ease;
}

.back-to-idea:hover {
  color: var(--cyan-dream);
}

/* Modal transition */
.modal-enter-active,
.modal-leave-active {
  transition: all 0.4s ease;
}

.modal-enter-from,
.modal-leave-to {
  opacity: 0;
}

.modal-enter-from .dream-modal,
.modal-leave-to .dream-modal {
  transform: scale(0.9) translateY(20px);
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

  .dream-modal {
    padding: 2rem 1.5rem;
  }

  .idea-name {
    font-size: 1.5rem;
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
