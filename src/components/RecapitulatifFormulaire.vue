<template>
    <div>
      <h2>Récapitulatif de l'inscription</h2>
      <p><strong>Email :</strong> {{ formData.email }}</p>
      <!-- Affichez ici les autres champs du formulaire -->
  
      <p><strong>Type d'inscription :</strong> {{ formData.typeOfRegistration }}</p>
      <p><strong>Mode d'hébergement :</strong> {{ formData.accommodation }}</p>
  
      <p><strong>Montant total :</strong> {{ calculateTotalAmount }} €</p>
    </div>
  </template>
  
  <script>
  export default {
    name: 'RecapitulatifFormulaire',
    props: {
      formData: {
        type: Object,
        required: true,
      },
    },
    computed: {
      calculateTotalAmount() {
        return formData.inscription + formData.hebergement;
      },
    },
  };
  </script>
  