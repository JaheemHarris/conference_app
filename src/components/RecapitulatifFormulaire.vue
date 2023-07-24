<template>
  <div class="row summary">
    <div class="title" style="background-color: rgb(207, 207, 207);">
      <p style="font-size: 1rem;">Récapitulatif de l'inscription</p>
    </div>
    <div class="content">
      <p>Bonjour {{ formData.sexe === 'H' ? 'monsieur' : 'madame' }} {{ `${formData.prenom} ${formData.nom}` }}, vous avez
        procédé à une inscription pour la conférence #MaConf2020.</p>
      <!-- Affichez ici les autres champs du formulaire -->

      <p>Le détail de votre enregistrement est le suivant:</p>
      <ul>
        <li>{{ getSelectedInscription.label }} {{ getSelectedInscription.montant }} EUR</li>
        <li>{{ getSelectedHebergement.label }} {{ getSelectedHebergement.montant }} EUR</li>
      </ul>

      <p>Le montant total est de {{ calculateTotalAmount }} EUR</p>
      <p>Un email vous sera envoyé prochainement à cette adresse {{ formData.emali }} pour la mise en paiement de votre
        inscription. <br>
        Merci de consulter votre messagerie et de procéder au règlement de votre inscription.
      </p>
      <p>En vous remerciant de votre inscription, à très bientôt à la conférence #MaConf2020.</p>
      <div class="content-buttons">
        <button class="btn btn-primary" type="button">Confirmer</button>
        <button class="btn btn-primary" type="button">Modifier les données</button>
      </div>
    </div>
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
  data() {
    const inscriptions = [
      {
        key: 1,
        label: "Etudiant",
        montant: 150
      },
      {
        key: 2,
        label: "Académique",
        montant: 200
      },
      {
        key: 3,
        label: "Entreprise",
        montant: 300
      },
    ];

    const hebergements = [
      {
        key: 1,
        label: 'Avec réservation',
        montant: 150
      },
      {
        key: 2,
        label: 'Sans réservation',
        montant: 0
      },
    ];
    return {
      hebergements,
      inscriptions
    }
  },
  computed: {
    getSelectedInscription() {
      return this.inscriptions.find((inscription) => parseFloat(inscription.montant) === parseFloat(this.formData.inscription));
    },
    getSelectedHebergement() {
      return this.hebergements.find((hebergement) => parseFloat(hebergement.montant) === parseFloat(this.formData.hebergement));
    },
    calculateTotalAmount() {
      return parseFloat(this.formData.inscription) + parseFloat(this.formData.hebergement);
    },
  },
};
</script>
  
<style scoped>
  .summary{
    margin-top: 2%;
    margin-bottom: 2%;
    border: 0.5px rgb(207, 207, 207) solid;
    border-radius: 5px 5px;
  }

  .content-buttons{
    margin-bottom: 2%;
  }

  .content-buttons button{
    margin-left: 5px;
    margin-right: 5px;
  }
</style>