<template>
  <div class="row justify-content-center">
    <form @submit.prevent="handleSubmit" class="col-lg-8 col-sm-10">
      <h2 class="text-center">Inscription pour #MaConf2020</h2>
      <!-- Affichage des erreurs -->
      <div v-if="hasErrors()" class="errors">
        <div class="errors-box">
          <div class="title" style="background-color: rgb(207, 207, 207);">
            <p style="font-size: 1rem;">Corrigez les erreurs suivantes:</p>
          </div>
          <div class="errors-content">
            <ul>
              <li v-for="error in errors()" :key="error.field">{{ error.message }}</li>
            </ul>
          </div>
        </div>
      </div>
      <div>
        <h3>Qui êtes vous?</h3>
        <div class="row">
          <div class="row justify-content-between">
            <div class="col-5">
              <label class="form-label" for="prenom">Prénom*</label>
              <input type="text" class="form-control" name="prenom" id="prenom" v-model="formData.prenom" :disabled="formSubmitted && !hasErrors()"/>
            </div>
            <div class="col-5">
              <label class="form-label" for="nom">Nom*</label>
              <input type="text" class="form-control" name="nom" id="nom" v-model="formData.nom" :disabled="formSubmitted && !hasErrors()"/>
            </div>
          </div>
          <div class="row">
            <div class="col-12">
              <label class="form-label" for="email">Adresse email*</label>
              <input type="email" class="form-control" name="email" id="email" v-model="formData.email" :disabled="formSubmitted && !hasErrors()"/>
            </div>
          </div>
          <div class="row">
            <div class="col-12">
              <label for="sexe-options" class="form-label">Sexe</label>
              <div id="sexe-options">
                <div class="form-check form-check-inline">
                  <input class="form-check-input" type="radio" name="sexe" id="inlineRadio1" value="H"
                    v-model="formData.sexe" :disabled="formSubmitted && !hasErrors()">
                  <label class="form-check-label" for="inlineRadio1">Je suis un homme</label>
                </div>
                <div class="form-check form-check-inline">
                  <input class="form-check-input" type="radio" name="sexe" id="inlineRadio2" value="F"
                    v-model="formData.sexe" :disabled="formSubmitted && !hasErrors()">
                  <label class="form-check-label" for="inlineRadio2">Je suis une femme</label>
                </div>
              </div>
            </div>
          </div>
          <div class="row">
            <div class="col-12">
              <label class="form-label" for="institution">Institution*</label>
              <input type="text" class="form-control" name="institution" id="institution"
                v-model="formData.institution" :disabled="formSubmitted && !hasErrors()"/>
            </div>
          </div>
          <div class="row justify-content-between">
            <div class="col-5">
              <label class="form-label" for="adresse">Adresse*</label>
              <input type="text" class="form-control" name="adresse" id="adresse" v-model="formData.adresse" :disabled="formSubmitted && !hasErrors()"/>
            </div>
            <div class="col-5">
              <label class="form-label" for="pays">Pays*</label>
              <input type="text" class="form-control" name="pays" id="pays" v-model="formData.pays" :disabled="formSubmitted && !hasErrors()"/>
            </div>
          </div>
          <div class="row justify-content-between">
            <div class="col-5">
              <label class="form-label" for="code_postal">Code Postal*</label>
              <input type="text" class="form-control" name="code_postal" id="code_postal" v-model="formData.codePostal" :disabled="formSubmitted && !hasErrors()"/>
            </div>
            <div class="col-5">
              <label class="form-label" for="ville">Ville*</label>
              <input type="text" class="form-control" name="ville" id="ville" v-model="formData.ville" :disabled="formSubmitted && !hasErrors()"/>
            </div>
          </div>
          <div class="row justify-content-between">
            <div class="col-5">
              <label class="form-label" for="page_web_personnelle">Page web personnelle</label>
              <input type="text" class="form-control" name="page_web_personnelle" id="page_web_personnelle"
                v-model="formData.pageWebPersonnelle" :disabled="formSubmitted && !hasErrors()"/>
            </div>
            <div class="col-5">
              <label class="form-label" for="page_web_institution">Page web institution</label>
              <input type="text" class="form-control" name="page_web_institution" id="page_web_institution"
                v-model="formData.pageWebInstitution" :disabled="formSubmitted && !hasErrors()"/>
            </div>
          </div>
        </div>
      </div>
      <hr>
      <div>
        <h3>Quelle inscription souhaitez-vous?</h3>
        <div class="row">
          <div class="form-check form-check-inline">
            <input class="form-check-input" type="radio" name="inscription" id="inlineRadio1" value="150"
              v-model="formData.inscription" :disabled="formSubmitted && !hasErrors()"/>
            <label class="form-check-label" for="inlineRadio1">Etudiant (150 EUR)</label>
          </div>
          <div class="form-check form-check-inline">
            <input class="form-check-input" type="radio" name="inscription" id="inlineRadio2" value="200"
              v-model="formData.inscription" :disabled="formSubmitted && !hasErrors()"/>
            <label class="form-check-label" for="inlineRadio2">Académique (200 EUR)</label>
          </div>
          <div class="form-check form-check-inline">
            <input class="form-check-input" type="radio" name="inscription" id="inlineRadio2" value="300"
              v-model="formData.inscription" :disabled="formSubmitted && !hasErrors()"/>
            <label class="form-check-label" for="inlineRadio2">Entreprise (300 EUR)</label>
          </div>
        </div>
      </div>
      <hr>
      <div>
        <h3>Quel hébergément souhaitez-vous?</h3>
        <div class="row">
          <div class="form-check form-check-inline">
            <input class="form-check-input" type="radio" name="hebergement" id="inlineRadio1" value="150"
              v-model="formData.hebergement" :disabled="formSubmitted && !hasErrors()"/>
            <label class="form-check-label" for="inlineRadio1">Avec réservation (150 EUR)</label>
          </div>
          <div class="form-check form-check-inline">
            <input class="form-check-input" type="radio" name="hebergement" id="inlineRadio2" value="0"
              v-model="formData.hebergement" :disabled="formSubmitted && !hasErrors()"/>
            <label class="form-check-label" for="inlineRadio2">Sans réservation (0 EUR)</label>
          </div>
        </div>
      </div>
      <hr>

      <button type="submit" class="btn btn-primary">Pré-valider</button>

      <RecapitulatifFormulaire v-if="showSummary" :formData="formData" />
    </form>
  </div>
</template>
  
<script>
import RecapitulatifFormulaire from "./RecapitulatifFormulaire.vue";

export default {
  name: 'FormulaireConference',
  components: {
    RecapitulatifFormulaire,
  },
  data() {
    const errorMessages = [
      {
        field: "prenom",
        message: "Prénom obligatoire",
      },
      {
        field: "nom",
        message: "Nom est obligatoire",
      },
      {
        field: "email",
        message: "Adresse email obligatoire",
      },
      {
        field: "institution",
        message: "Institution est obligatoire",
      },
      {
        field: "codePostal",
        message: "Code Postal est obligatoire",
      },
      {
        field: "pays",
        message: "Pays est obligatoire",
      },
      {
        field: "adresse",
        message: "Adresse est obligatoire",
      },
      {
        field: "ville",
        message: "Ville est obligatoire",
      },
      {
        field: "inscription",
        message: "Formulaire d'inscription obligatoire",
      },
      {
        field: "hebergement",
        message: "Moyen d'hébergement obligatoire",
      },
    ];

    return {
      showSummary: false,
      formSubmitted: false,
      errorMessages,
      formData: {
        prenom: "",
        nom: "",
        email: "",
        sexe: "",
        institution: "",
        codePostal: "",
        pays: "",
        adresse: "",
        ville: "",
        pageWebInstitution: "",
        pageWebPersonnelle: "",
      },
    };
  },
  methods: {
    hasErrors() {
      return this.formSubmitted && this.errorMessages.some(({ field }) => !this.formData[field]);
    },
    errors() {
      return this.errorMessages
        .filter(({ field }) => !this.formData[field]);
    },
    handleSubmit() {
      console.log(this.formData);
      this.formSubmitted = true;
      if (!this.hasErrors()) {
        this.showSummary = true;
      } else {
        this.showSummary = false;
      }
      console.log(this.errors());
    },
  },
};
</script>

<style scoped>
.errors-box {
  margin-top: 2%;
  margin-bottom: 2%;
  border: 0.5px rgb(207, 207, 207) solid;
  border-radius: 5px 5px;
}
</style>