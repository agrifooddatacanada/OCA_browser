<template>
  <q-page class="q-pa-md">
    <q-card class="training-card">
      <q-card-section>
        <div class="text-h5">Training</div>
      </q-card-section>
      <q-separator />
      <q-card-section>
        <p>
          A training pathway for researchers to generate a usable data schema is
          being created by
          <a href="https://agrifooddatacanada.ca/">Agri-Food Data Canada</a>.
          Step-by-step instructions could be found below.
        </p>
      </q-card-section>
      <q-separator />
      <q-card-section>
        <q-card class="markdown-body q-pa-md">
          <h1 id="a-pathway-for-creating-data-schemas">
            A pathway for creating data schemas
          </h1>
          <p>
            Schemas are a way to document your data and help make it more FAIR
            (Findable, Accessible, Interoperable, Reusable). Creating a schema
            is a process of continuous improvement. You don&#39;t need to create
            the most perfect and complete schema at the beginning. Instead,
            follow this pathway to gradual improvement where each step produces
            something usable for researchers.
          </p>
          <p>
            <a
              href="https://forms.office.com/Pages/ResponsePage.aspx?id=K6Fivq0soUml-oX08xVqfcxKJkze2nVHnEbvp9MCrIhUMjY3R0tTUDRTTU42RlBXMlAzRzdTSlo3RiQlQCN0PWcu"
              >Feedback for creating a schema can be done in this Form</a
            >.
          </p>
          <h1 id="1-introduction-to-the-rationale">
            1. Introduction to the rationale
          </h1>
          <div class="row justify-center">
            <q-btn
              type="a"
              color="primary"
              label="Access the Tutorials"
              href="https://agrifooddatacanada.github.io/OCA_training_pathway" />
          </div>
        </q-card>
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script lang="ts">
import { defineComponent } from 'vue'

export default defineComponent({
  name: 'Training'
})
</script>

<style lang="scss">
@import '/node_modules/github-markdown-css/github-markdown-light.css';
.training-card {
  min-width: 300px;
  width: min(700px, 100%);
}
</style>
