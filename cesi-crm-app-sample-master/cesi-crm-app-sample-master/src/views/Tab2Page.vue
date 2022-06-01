<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Contact</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-header collapse="condense">
        <ion-toolbar>
          <ion-title size="large">Contact</ion-title>
        </ion-toolbar>
      </ion-header>
      <ion-card>
        <ion-card-header>
          <ion-card-subtitle>Liste des contacts</ion-card-subtitle>
          <ion-card-title>Ma liste des contacts</ion-card-title>
        </ion-card-header>
        <div v-if="contacts.length > 0">
        <div v-for="(contact, index) in contacts" :key="index">
        <ion-accordion-group>
          <ion-accordion value="colors">
            <ion-item slot="header">
              <ion-label>Nom : {{ contact.name }}</ion-label>
            </ion-item>
              <ion-list slot="content">
              <ion-item>
                <ion-label>Nom : {{ contact.name }}</ion-label>
              </ion-item>
              <ion-item>
                <ion-label>Prénom : {{ contact.firstname }}</ion-label>
              </ion-item>
              <ion-item>
                <ion-label>Adresse : {{ contact.address }}</ion-label>
              </ion-item>
              <ion-item>
                <ion-label>Entreprise : {{ contact.company }}</ion-label>
              </ion-item>
              <ion-item>
                <ion-label>Téléphone : {{ contact.phoneNumber }}</ion-label>
              </ion-item>
              <ion-item>
                <ion-label>Email : {{ contact.email }}</ion-label>
              </ion-item>
              <ion-item>
                <ion-label>Note : {{ contact.note }}</ion-label>
              </ion-item>
              <ion-item>
                <ion-label>
                  <ion-button @click="updateContact(index)" expand="block">Modifier le contact</ion-button>
                  <ion-button @click="deleteContact(index)" expand="block">Supprimer le contact</ion-button>
                </ion-label>
              </ion-item>
            </ion-list>
          </ion-accordion>
        </ion-accordion-group>
        </div></div>
        <div v-else>
          <p style="color: red;">Vous n'avez pas de contact pour le moment</p>
        </div>
      </ion-card>      
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent } from '@ionic/vue';
import contactQuery from '../query/contact.query';
import { Contact } from '../domains/contact.interface';
//import contactCommand from '../commands/contact.command';

export default defineComponent({
  name: 'Tab2Page',
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage },
    data() {
    return {
      contacts: [] as Array<Contact>
    }
  },
  mounted() {
    this.getContacts();
  },
    methods: {
    getContacts() {
      this.contacts = contactQuery.getContacts();
    },
    deleteContact(index) {
      this.contacts.splice(this.contacts.index, 6);
      this.getContacts();
    }/*,
    updateContact(index) {
      this.contacts.splice(index, 6, );
      this.getContacts();      
    }*/
}});
</script>
