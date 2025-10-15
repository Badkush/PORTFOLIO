<template>
    <section id="contact" class="contact">
        <div class="container">
            <div class="contact-header">
                <h2 class="section-title">Contactez-moi</h2>
                <p class="section-subtitle">
                    Vous avez un projet en tête ? N'hésitez pas à me contacter pour en discuter !
                </p>
            </div>

            <div class="contact-content">
                <!-- Informations de contact -->
                <div class="contact-info">
                    <h3 class="info-title">Informations de contact</h3>
                    
                    <div class="contact-item">
                        <div class="contact-icon">
                            <svg viewBox="0 0 24 24" fill="currentColor">
                                <path d="M20 4H4c-1.1 0-1.99.9-1.99 2L2 18c0 1.1.9 2 2 2h16c1.1 0 2-.9 2-2V6c0-1.1-.9-2-2-2zm0 4l-8 5-8-5V6l8 5 8-5v2z"/>
                            </svg>
                        </div>
                        <div class="contact-details">
                            <h4>Email</h4>
                            <a href="mailto:maxcuche46@gmail.com">maxcuche46@gmail.com</a>
                        </div>
                    </div>

                    <div class="contact-item">
                        <div class="contact-icon">
                            <svg viewBox="0 0 24 24" fill="currentColor">
                                <path d="M12 2C8.13 2 5 5.13 5 9c0 5.25 7 13 7 13s7-7.75 7-13c0-3.87-3.13-7-7-7zm0 9.5c-1.38 0-2.5-1.12-2.5-2.5s1.12-2.5 2.5-2.5 2.5 1.12 2.5 2.5-1.12 2.5-2.5 2.5z"/>
                            </svg>
                        </div>
                        <div class="contact-details">
                            <h4>Localisation</h4>
                            <p>Mercues, Lot (46)</p>
                        </div>
                    </div>

                    <div class="contact-item">
                        <div class="contact-icon">
                            <svg viewBox="0 0 24 24" fill="currentColor">
                                <path d="M19.615 3.184c-3.604-.246-11.631-.245-15.23 0-3.897.266-4.356 2.62-4.385 8.816.029 6.185.484 8.549 4.385 8.816 3.6.245 11.626.246 15.23 0 3.897-.266 4.356-2.62 4.385-8.816-.029-6.185-.484-8.549-4.385-8.816zm-10.615 12.816v-8l8 3.993-8 4.007z"/>
                            </svg>
                        </div>
                        <div class="contact-details">
                            <h4>GitHub</h4>
                            <a href="https://github.com/Badkush" target="_blank">github.com/Badkush</a>
                        </div>
                    </div>
                </div>

                <!-- Formulaire de contact -->
                <div class="contact-form-container">
                    <form @submit.prevent="submitForm" class="contact-form">
                        <div class="form-group">
                            <label for="name">Nom complet *</label>
                            <input
                                type="text"
                                id="name"
                                v-model="form.name"
                                :class="{ 'error': errors.name }"
                                placeholder="Votre nom complet"
                                required
                            />
                            <span v-if="errors.name" class="error-message">{{ errors.name }}</span>
                        </div>

                        <div class="form-group">
                            <label for="email">Email *</label>
                            <input
                                type="email"
                                id="email"
                                v-model="form.email"
                                :class="{ 'error': errors.email }"
                                placeholder="votre.email@exemple.com"
                                required
                            />
                            <span v-if="errors.email" class="error-message">{{ errors.email }}</span>
                        </div>

                        <div class="form-group">
                            <label for="company">Entreprise</label>
                            <input
                                type="text"
                                id="company"
                                v-model="form.company"
                                placeholder="Votre entreprise (optionnel)"
                            />
                        </div>

                        <div class="form-group">
                            <label for="subject">Sujet *</label>
                            <select
                                id="subject"
                                v-model="form.subject"
                                :class="{ 'error': errors.subject }"
                                required
                            >
                                <option value="">Sélectionnez un sujet</option>
                                <option value="website">Site web vitrine</option>
                                <option value="webapp">Application web</option>
                                <option value="mobile">Application mobile</option>
                                <option value="design">Design UI/UX</option>
                                <option value="maintenance">Maintenance</option>
                                <option value="other">Autre</option>
                            </select>
                            <span v-if="errors.subject" class="error-message">{{ errors.subject }}</span>
                        </div>

                        <div class="form-group">
                            <label for="budget">Budget estimé</label>
                            <select id="budget" v-model="form.budget">
                                <option value="">Sélectionnez une fourchette</option>
                                <option value="500-1000">500€ - 1 000€</option>
                                <option value="1000-2500">1 000€ - 2 500€</option>
                                <option value="2500-5000">2 500€ - 5 000€</option>
                                <option value="5000+">Plus de 5 000€</option>
                            </select>
                        </div>

                        <div class="form-group">
                            <label for="deadline">Délais souhaités</label>
                            <input
                                type="text"
                                id="deadline"
                                v-model="form.deadline"
                                placeholder="Ex: Dans 2 mois, Urgent, Flexible..."
                            />
                        </div>

                        <div class="form-group">
                            <label for="message">Message *</label>
                            <textarea
                                id="message"
                                v-model="form.message"
                                :class="{ 'error': errors.message }"
                                placeholder="Décrivez votre projet en détail..."
                                rows="6"
                                required
                            ></textarea>
                            <span v-if="errors.message" class="error-message">{{ errors.message }}</span>
                        </div>

                        <div class="form-actions">
                            <button
                                type="submit"
                                class="submit-btn"
                                :disabled="isSubmitting"
                            >
                                <span v-if="!isSubmitting">
                                    <svg viewBox="0 0 24 24" fill="currentColor">
                                        <path d="M2.01 21L23 12 2.01 3 2 10l15 2-15 2z"/>
                                    </svg>
                                    Envoyer le message
                                </span>
                                <span v-else>
                                    Envoi en cours...
                                </span>
                            </button>
                        </div>
                    </form>
                </div>
            </div>
        </div>
    </section>
</template>

<script setup>
import { ref, reactive } from 'vue'

// État du formulaire
const form = reactive({
  name: '',
  email: '',
  company: '',
  subject: '',
  budget: '',
  deadline: '',
  message: ''
})

// Erreurs de validation
const errors = reactive({
  name: '',
  email: '',
  subject: '',
  message: ''
})

// État de soumission
const isSubmitting = ref(false)

// Fonction de validation
const validateForm = () => {
  // Réinitialiser les erreurs
  Object.keys(errors).forEach(key => {
    errors[key] = ''
  })

  let isValid = true

  // Validation du nom
  if (!form.name.trim()) {
    errors.name = 'Le nom est obligatoire'
    isValid = false
  } else if (form.name.trim().length < 2) {
    errors.name = 'Le nom doit contenir au moins 2 caractères'
    isValid = false
  }

  // Validation de l'email
  const emailRegex = /^[^\s@]+@[^\s@]+\.[^\s@]+$/
  if (!form.email.trim()) {
    errors.email = 'L\'email est obligatoire'
    isValid = false
  } else if (!emailRegex.test(form.email)) {
    errors.email = 'Veuillez entrer un email valide'
    isValid = false
  }

  // Validation du sujet
  if (!form.subject) {
    errors.subject = 'Veuillez sélectionner un sujet'
    isValid = false
  }

  // Validation du message
  if (!form.message.trim()) {
    errors.message = 'Le message est obligatoire'
    isValid = false
  } else if (form.message.trim().length < 10) {
    errors.message = 'Le message doit contenir au moins 10 caractères'
    isValid = false
  }

  return isValid
}

// Fonction de soumission du formulaire
const submitForm = async () => {
  if (!validateForm()) {
    return
  }

  isSubmitting.value = true

  try {
    // Simulation d'envoi d'email (remplacez par votre API)
    await new Promise(resolve => setTimeout(resolve, 2000))

    // Construire l'email
    const emailData = {
      to: 'maxcuche46@gmail.com',
      subject: `Nouveau contact - ${form.subject}`,
      body: `
Nouveau message de contact depuis votre portfolio

Nom: ${form.name}
Email: ${form.email}
${form.company ? `Entreprise: ${form.company}` : ''}
Sujet: ${form.subject}
${form.budget ? `Budget: ${form.budget}` : ''}
${form.deadline ? `Délais: ${form.deadline}` : ''}

Message:
${form.message}
      `.trim()
    }

    // Ouvrir le client email par défaut
    const mailtoUrl = `mailto:${emailData.to}?subject=${encodeURIComponent(emailData.subject)}&body=${encodeURIComponent(emailData.body)}`
    window.location.href = mailtoUrl

    // Afficher un message de succès
    alert('Merci pour votre message ! Votre client email va s\'ouvrir avec le message pré-rempli.')

    // Réinitialiser le formulaire
    Object.keys(form).forEach(key => {
      form[key] = ''
    })

  } catch (error) {
    alert('Une erreur est survenue. Veuillez réessayer ou me contacter directement à maxcuche46@gmail.com')
  } finally {
    isSubmitting.value = false
  }
}
</script>

<style scoped>
.contact {
  background: linear-gradient(135deg, #FFFEEF 0%, #f8f4e6 100%);
  padding: 80px 0;
  min-height: 100vh;
}

.container {
  max-width: 1200px;
  margin: 0 auto;
  padding: 0 20px;
}

.contact-header {
  text-align: center;
  margin-bottom: 60px;
}

.section-title {
  font-size: 2.5rem;
  margin-bottom: 20px;
  color: #F20E0E;
  font-weight: bold;
  text-transform: uppercase;
  letter-spacing: 2px;
}

.section-subtitle {
  font-size: 1.1rem;
  color: #F20E0E;
  max-width: 600px;
  margin: 0 auto;
  line-height: 1.6;
}

.contact-content {
  display: grid;
  grid-template-columns: 1fr 2fr;
  gap: 60px;
  align-items: start;
}

/* Section informations de contact */
.contact-info {
  background: white;
  padding: 40px;
  border-radius: 15px;
  box-shadow: 0 10px 30px rgba(242, 14, 14, 0.1);
  height: fit-content;
}

.info-title {
  font-size: 1.5rem;
  color: #F20E0E;
  margin-bottom: 30px;
  font-weight: bold;
}

.contact-item {
  display: flex;
  align-items: center;
  gap: 20px;
  margin-bottom: 30px;
  padding: 20px;
  border-radius: 10px;
  transition: background-color 0.3s ease;
}

.contact-item:hover {
  background-color: #f8f9fa;
}

.contact-icon {
  width: 50px;
  height: 50px;
  background: linear-gradient(135deg, #F20E0E, #ff4757);
  border-radius: 50%;
  display: flex;
  align-items: center;
  justify-content: center;
  color: white;
  flex-shrink: 0;
}

.contact-icon svg {
  width: 24px;
  height: 24px;
}

.contact-details h4 {
  font-size: 1.1rem;
  color: #333;
  margin-bottom: 5px;
  font-weight: 600;
}

.contact-details p,
.contact-details a {
  color: #666;
  text-decoration: none;
  font-size: 0.95rem;
}

.contact-details a:hover {
  color: #F20E0E;
}

/* Formulaire de contact */
.contact-form-container {
  background: white;
  padding: 40px;
  border-radius: 15px;
  box-shadow: 0 10px 30px rgba(242, 14, 14, 0.1);
}

.contact-form {
  display: grid;
  gap: 25px;
}

.form-group {
  display: flex;
  flex-direction: column;
}

.form-group label {
  font-weight: 600;
  color: #333;
  margin-bottom: 8px;
  font-size: 0.95rem;
}

.form-group input,
.form-group select,
.form-group textarea {
  padding: 12px 16px;
  border: 2px solid #e0e0e0;
  border-radius: 8px;
  font-size: 1rem;
  transition: all 0.3s ease;
  font-family: inherit;
}

.form-group input:focus,
.form-group select:focus,
.form-group textarea:focus {
  outline: none;
  border-color: #F20E0E;
  box-shadow: 0 0 0 3px rgba(242, 14, 14, 0.1);
}

.form-group input.error,
.form-group select.error,
.form-group textarea.error {
  border-color: #dc3545;
  box-shadow: 0 0 0 3px rgba(220, 53, 69, 0.1);
}

.form-group textarea {
  resize: vertical;
  min-height: 120px;
}

.error-message {
  color: #dc3545;
  font-size: 0.85rem;
  margin-top: 5px;
  font-weight: 500;
}

.form-actions {
  margin-top: 20px;
}

.submit-btn {
  background: linear-gradient(135deg, #F20E0E, #ff4757);
  color: white;
  border: none;
  padding: 15px 30px;
  border-radius: 8px;
  font-size: 1rem;
  font-weight: 600;
  cursor: pointer;
  transition: all 0.3s ease;
  display: inline-flex;
  align-items: center;
  gap: 10px;
  text-transform: uppercase;
  letter-spacing: 0.5px;
}

.submit-btn:hover:not(:disabled) {
  transform: translateY(-2px);
  box-shadow: 0 8px 25px rgba(242, 14, 14, 0.3);
}

.submit-btn:disabled {
  opacity: 0.7;
  cursor: not-allowed;
  transform: none;
}

.submit-btn svg {
  width: 18px;
  height: 18px;
}

/* Responsive Design */
@media (max-width: 768px) {
  .contact-content {
    grid-template-columns: 1fr;
    gap: 40px;
  }
  
  .contact-info,
  .contact-form-container {
    padding: 30px 20px;
  }
  
  .section-title {
    font-size: 2rem;
  }
  
  .contact-item {
    flex-direction: column;
    text-align: center;
    gap: 15px;
  }
  
  .contact-icon {
    margin: 0 auto;
  }
}

@media (max-width: 480px) {
  .contact {
    padding: 40px 0;
  }
  
  .container {
    padding: 0 15px;
  }
  
  .section-title {
    font-size: 1.6rem;
    letter-spacing: 1px;
  }
  
  .contact-info,
  .contact-form-container {
    padding: 20px 15px;
  }
}
</style>