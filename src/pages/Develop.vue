<template>
  <q-page class="q-pa-md">
   <!--<q-card-section>
      <div class="text-h5">OCA Composer</div>
        <q-card-section class="text-subitle2">
          Visit <a href="https://ocacomposer.semanticengine.org>OCA Composer</a> to create an Excel Template for your schema using a web interface.</br>
          Here you can also edit .zip schema bundles, and generate a plain text Readme file of your schema.
        </q-card-section>
    </q-card-section> -->

    <q-separator />
    <q-card class="converter-card">
      <q-card-section>
        <div class="row">
          <div class="text-h5">Excel Template to OCA Schema Bundle Converter</div>
          <q-btn
            color="grey"
            round
            flat
            dense
            :icon="converterHelpExpanded ? 'help_outline' : 'help'"
            @click="converterHelpExpanded = !converterHelpExpanded" />
        </div>
      </q-card-section>

      <q-slide-transition>
        <div v-show="converterHelpExpanded">
          <q-separator />
          <q-card-section class="text-subitle2">
            Use this parser to convert from a properly prepared Excel Schema Template file to an OCA Schema Bundle.<br />
            As an outcome you would receive a zip file with your schema.<br />
            The zip file is the machine-readable version of your schema which you can store together with your data or upload into a repository for reference.<br />
            <ul>
              <li>
                <b>OCA Excel Template [required] (XLS/XLSX)</b><br />
                <a
                  href="https://github.com/agrifooddatacanada/OCA_training_pathway/raw/main/templates/UoG_SchemaTemplate_Latest.xlsx">
                  Download template</a>.
              </li>
              <li>
                 <b>Data Entry File</b><br />
                 An Excel file, ready for data entry, and with labels and descriptions taken from your schema.
              </li>
            </ul>
          </q-card-section>
        </div>
      </q-slide-transition>

      <q-separator />

      <q-card-section>
        <q-file
          v-model="rootFile"
          label="Select Excel Template file"
          accept=".xls,.xlsx"
          filled />
        <!-- <q-file
          v-model="referenceFiles"
          label="Select OCA references files"
          accept=".xls,.xlsx"
          multiple /> -->

        <q-checkbox
          v-model="withDataEntry"
          size="lg"
          label="Generate Data Entry File" />

        <!-- <br /> -->

        <!-- <q-checkbox
          v-model="withArchive"
          size="lg"
          label="Generate Archive Text Format" /> -->

        <br />

        <q-btn color="primary" :disable="!rootFile" @click="convert">
          Convert
        </q-btn>
        <br />
        <!-- eslint-disable vue/no-v-html -->
        <span v-html="convertionResult" />
        <!-- eslint-enable vue/no-v-html -->
      </q-card-section>
    </q-card>
  </q-page>
</template>

<script lang="ts">
import { defineComponent, ref, watch, getCurrentInstance } from 'vue'
import { AxiosInstance } from 'axios'

export default defineComponent({
  name: 'Develop',
  setup() {
    const currentInstance = getCurrentInstance()
    if (!currentInstance) {
      return
    }
    const $axios = currentInstance.appContext.config.globalProperties
      .$axios as AxiosInstance
    const converterHelpExpanded = ref(true)
    const rootFile = ref()
    const referenceFiles = ref([])
    const withDefaultCredentialLayout = ref(false)
    const credentialLayoutFile = ref()
    const withDefaultFormLayout = ref(false)
    const formLayoutFile = ref()
    const withDataEntry = ref(false)
    const withArchive = ref(false)
    const convertionResult = ref('')

    const ocaConverterUrl = 'https://tool.oca.argo.colossi.network'

    watch(withDefaultCredentialLayout, value => {
      if (value) {
        credentialLayoutFile.value = null
      }
    })
    watch(credentialLayoutFile, newFile => {
      if (newFile) {
        withDefaultCredentialLayout.value = false
      }
    })
    watch(withDefaultFormLayout, value => {
      if (value) {
        formLayoutFile.value = null
      }
    })
    watch(formLayoutFile, newFile => {
      if (newFile) {
        withDefaultFormLayout.value = false
      }
    })

    /* eslint-disable */
    const convert = async () => {
      const formData = new FormData()
      formData.append('file', rootFile.value)
      referenceFiles.value.forEach((file: File) =>
        formData.append('referencesFiles[]', file)
      )

      if (credentialLayoutFile.value) {
        formData.append('credentialLayoutFile', credentialLayoutFile.value)
      }
      if (formLayoutFile.value) {
        formData.append('formLayoutFile', formLayoutFile.value)
      }

      formData.append('withDefaultCredentialLayout', ""+withDefaultCredentialLayout.value)
      formData.append('withDefaultFormLayout', ""+withDefaultFormLayout.value)
      formData.append('withDataEntry', ""+withDataEntry.value)
      formData.append('withArchive', ""+withArchive.value)

      const response = await $axios.post(ocaConverterUrl, formData)
      const responseResult = response.data
      if (responseResult.success) {
        convertionResult.value = `Success!<ul><li><a href="${ocaConverterUrl}/${responseResult.filename}">Click here to download OCA Bundle</a></li>`
        if (withDataEntry.value) {
          convertionResult.value += `<li><a href="${ocaConverterUrl}/${responseResult.data_entry}">Click here to download OCA Data Entry file</a></li>`
        }
        convertionResult.value += `</ul>`
      } else {
        const errors: string[] = responseResult.errors
        console.error(errors)
        convertionResult.value = 'Failure! Fix those errors and try again: <ul>'
        errors.forEach(e => convertionResult.value += `<li>${e}</li>`)
        convertionResult.value += '</ul>'
      }

      resetForm()
    }
    /* eslint-enable */

    const resetForm = () => {
      rootFile.value = null
      referenceFiles.value = []
      withDefaultCredentialLayout.value = false
      credentialLayoutFile.value = null
      withDefaultFormLayout.value = false
      formLayoutFile.value = null
      withDataEntry.value = false
      withArchive.value = false
    }

    return {
      convert,
      converterHelpExpanded,
      convertionResult,
      rootFile,
      referenceFiles,
      withDefaultCredentialLayout,
      credentialLayoutFile,
      withDefaultFormLayout,
      formLayoutFile,
      withDataEntry,
      withArchive
    }
  }
})
</script>

<style>
.converter-card {
  min-width: 300px;
  width: min(700px, 100%);
}
</style>
