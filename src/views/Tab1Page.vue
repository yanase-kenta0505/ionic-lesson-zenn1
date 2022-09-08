<template>
  <ion-page>
    <ion-header>
      <ion-toolbar>
        <ion-title>Tab 1</ion-title>
      </ion-toolbar>
    </ion-header>
    <ion-content :fullscreen="true">
      <ion-button @click="showAlert('ボタンが押されました')">ボタン</ion-button>
    </ion-content>
  </ion-page>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import { IonPage, IonHeader, IonToolbar, IonTitle, IonContent, IonButton } from '@ionic/vue';
import { LocalNotifications } from '@capacitor/local-notifications'

export default defineComponent({
  name: 'Tab1Page',
  components: { IonHeader, IonToolbar, IonTitle, IonContent, IonPage, IonButton },


  setup() {
    const showAlert = async (msg: string) => {
      const date = new Date(Date.now() + 5000)
      await LocalNotifications.schedule({
        notifications: [
          {
            title: "通知です",
            body: `${msg}`,
            id: 1,
            schedule: { at: date },
            actionTypeId: "",
            extra: null,
          },
        ]
      })
      alert(msg)
    }


    return {
      showAlert
    }
  }
});
</script>
