<template>
  <q-page class="q-pa-md">
    <q-card class="about-card">
      <q-card-section>
        <div class="text-h5">About</div>
      </q-card-section>
      <q-separator />
      <q-card-section>
        <div class="text-h6">About ADC</div>
      </q-card-section>
      <q-card-section>
        <p>
          <a href="https://agrifooddatacanada.ca/"
            >Agri-food Data Canada (ADC)</a
          >
          is creating a data ecosystem serving agri-food sustainability. Through
          investments in technology, infrastructure and culture, we are helping
          researchers and the research community get more value from the data
          researchers are already collecting.
        </p>
        <p>
          ADC is currently being incubated within
          <a href="https://foodfromthought.ca/">Food from Thought</a>, a
          research program led by the
          <a href="https://www.uoguelph.ca/">University of Guelph</a> and funded
          by a $76.6-million grant from the
          <a href="https://www.cfref-apogee.gc.ca/home-accueil-eng.aspx"
            >Canada First Research Excellence Fund</a
          >. The program is intended to increase the sustainability and
          productivity of global food production by leveraging the power of
          leading-edge data science, agri-food research, and biodiversity
          science. Food from Thought will position Canada as a global leader in
          the development of innovative solutions that improve both the
          sustainability and the productivity of food systems at global,
          landscape, and micro levels.
        </p>
      </q-card-section>
      <q-separator />
      <q-card-section>
        <div class="text-h6">About Semantic Engine</div>
      </q-card-section>
      <q-card-section>
        <p>
          Semantics is a branch of linguistics and logic concerned with meaning.
          The Semantic Engine is a set of tools being developed at ADC helping
          researchers generate machine-accessible meaning for their data. One of
          the first tools we are developing will help researchers more easily
          create and use data schemas using the Overlays Capture Architecture
          (OCA) language for data schemas.
        </p>
        <p>
          You could find a step-by-step instructions for creating an OCA schema
          at the
          <a href="https://agrifooddatacanada.github.io/OCA_training_pathway/"
            >Training Pathway by ADC</a
          >.
        </p>
      </q-card-section>
      <q-separator />
      <q-card-section>
        <div class="text-h6">About OCA</div>
      </q-card-section>
      <q-card-section>
        <p>
          To create the semantic engine, ADC is partnering with the
          <a href="https://humancolossus.foundation/"
            >Human Colossus Foundation (HCF)</a
          >
          to adopt the HCF’s work on
          <a href="https://oca.colossi.network/"
            >overlays capture architecture (OCA)</a
          >
          as the underlying schema standard. Overlays capture architecture is an
          extensible, flexible, international, open, and machine-accessible
          standard for schemas.
        </p>
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'About'
})
</script>

<style lang="scss">
.about-card {
  min-width: 300px;
  width: min(700px, 100%);
}
</style>
