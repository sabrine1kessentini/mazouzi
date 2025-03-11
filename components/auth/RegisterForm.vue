<script setup lang="ts">
import { ref, watch } from 'vue';
const checkbox = ref(false);
const role = ref(''); // Pour stocker la valeur sélectionnée du rôle
const roles = ['Client', 'Prestataire de service']; // Liste des rôles disponibles
// Champs spécifiques aux prestataires de service
const service = ref(''); // Service proposé
type CategoryKey = keyof typeof subCategories;
const category = ref<CategoryKey>('Plomberie'); // Catégorie sélectionnée
const subCategory = ref(''); // Sous-catégorie sélectionnée

// Options pour les catégories et sous-catégories
const categories = ['Plomberie', 'Electricité', 'Climatisation', 'Autres'];
const subCategories = {
  Plomberie: ['Installation sanitaire', 'Fuites deau'],
  Electricité: ['Installation électrique', 'Dépannage'],
} as const;

// Observer les changements de rôle pour afficher/masquer les champs
watch(role, (newRole: string) => {
  if (newRole !== 'Prestataire de service') {
    service.value = '';
    category.value = 'Plomberie';
    subCategory.value = '';
  }
});
</script>
<template>
 
    <v-row class="d-flex  mb-3">

        <v-col cols="12">
            <v-label class="font-weight-medium mb-1">Name</v-label>
            <v-text-field variant="outlined" hide-details color="primary"></v-text-field>
        </v-col>
        <v-col cols="12">
            <v-label class="font-weight-medium mb-1">Email Address</v-label>
            <v-text-field variant="outlined" type="email" hide-details color="primary"></v-text-field>
        </v-col>
        <v-col cols="12">
            <v-label class="font-weight-medium mb-1">Password</v-label>
            <v-text-field variant="outlined" type="password"  hide-details color="primary"></v-text-field>
        </v-col>
        <v-col cols="12">
            <v-label class="font-weight-medium mb-1">Role</v-label>
            <v-select
                v-model="role"
                :items="roles"
                variant="outlined"
                hide-details
                color="primary"
                label="Select your role"
            ></v-select>
        </v-col>
          <!-- Champs spécifiques aux prestataires de service -->
    <template v-if="role === 'Prestataire de service'">
      <!-- Champ Service -->
      <v-col cols="12">
        <v-label class="font-weight-medium mb-1">Service</v-label>
        <v-text-field
          v-model="service"
          variant="outlined"
          hide-details
          color="primary"
          placeholder="Entrez le service que vous proposez"
        ></v-text-field>
      </v-col>

      <!-- Champ Catégorie -->
      <v-col cols="12">
        <v-label class="font-weight-medium mb-1">Catégorie</v-label>
        <v-select
          v-model="category"
          :items="categories"
          variant="outlined"
          hide-details
          color="primary"
          label="Choisissez une catégorie"
        ></v-select>
      </v-col>

      <!-- Champ Sous-catégorie -->
      <v-col cols="12" v-if="category">
        <v-label class="font-weight-medium mb-1">Sous-catégorie</v-label>
        <v-select
          v-model="subCategory"
          :items="subCategories[category]"
          variant="outlined"
          hide-details
          color="primary"
          label="Choisissez une sous-catégorie"
        ></v-select>
      </v-col>
    </template>
        <v-col cols="12" >
            <v-btn to="/" color="primary" rounded="pill" size="large" block   flat>Sign up</v-btn>
        </v-col>
    </v-row>
</template>
