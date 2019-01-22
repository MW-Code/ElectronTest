<template>
  <q-page class="flex flex-center">
<q-card>
  <q-list>
    <q-item>
      <q-item-side>
        <q-item-tile color="primary" icon="today" />
      </q-item-side>
      <q-item-main>
        <q-item-tile placeholder="dd.mm.yyyy" label>Dein Geburtsdatum</q-item-tile>
        <q-input v-model="bday"/>
      </q-item-main>
    </q-item>
    <q-item>
      <q-item-side>
        <q-item-tile color="red" icon="face" />
      </q-item-side>
      <q-item-main>
        <q-item-tile label>Dein Alter</q-item-tile>
        <q-input v-model="alter" type="number"/>
      </q-item-main>
    </q-item>
    <q-item>
      <q-item-main>
     <q-btn label="Check" color="primary" @click="calcBday" class="fit"/>
      </q-item-main>
    </q-item>
  </q-list>
</q-card>
  </q-page>
</template>

<style>
</style>

<script>
import { date } from 'quasar';


export default {
  name: 'PageIndex',
  data() {
    return {
      alter: '',
      bday: '',
    };
  },
  methods: {
    calcBday() {
      console.log('checke datum und alter');
      if (this.bday !== '') {
        console.log('berechne aus bday das alter');
        const date1 = new Date();
        const myRegexp = /^(\d\d).(\d\d).(\d\d\d\d)/;
        const match = myRegexp.exec(this.bday);
        const newDate = date.buildDate({
          year: match[3], date: match[1], month: match[2],
        });
        const unit = 'years';
        const diff = date.getDateDiff(date1, newDate, unit);
        this.alter = diff;
        return;
      }
      if (this.alter !== '') {
        console.log('berechne aus alter aus badayjahr');
        // const heute = new Date();
        let newDate = new Date();
        newDate = date.subtractFromDate(newDate, { year: this.alter });
        this.bday = date.formatDate(newDate, 'DD.MM.YYYY');
        console.log(newDate);
      }
    },
  },
};
</script>

<style scoped>

.datainput{
  width: 30px;
}

</style>

