<template>
  <v-row justify="center" align="center">
    <v-col cols="12" sm="10" md="10">
      <v-card>
        <v-card-title class="headline">
          Lindo to excel converter
        </v-card-title>
        <v-card-text>
          <v-form>
            <v-textarea
              v-model="input"
              :error-messages="error"
              autofocus
              label="Lindo tableau"
              height="350"
              outlined
            />
            <v-switch v-model="convertDotIntoComma" label="Convert dot (.) into comma (,)" class="mt-0" />
          </v-form>
        </v-card-text>
        <v-card-actions>
          <v-spacer />
          <v-btn color="primary" @click="clickConvert">Convert</v-btn>
        </v-card-actions>
      </v-card>
    </v-col>
  </v-row>
</template>

<script>
import exportFromJSON from 'export-from-json'
export default {
  name: 'IndexPage',
  data() {
    return {
      error: null,
      convertDotIntoComma: true,
      input: 'THE TABLEAU\n' +
        '\n' +
        '      ROW  (BASIS)         X1        X2  SLK    2  SLK    3  SLK    4\n' +
        '        1 ART           0.000     0.000     4.000     0.321     0.000   921.429\n' +
        '        2       X2      0.000     1.000     1.000    -0.057     0.000    92.857\n' +
        '        3       X1      1.000     0.000     0.000     0.057     0.000    57.143\n' +
        '        4 SLK    4      0.000     0.000   -10.000     0.571     1.000    71.429',
    }
  },
  methods: {
    getFileName() {
      return 'Lindo to excel - ' + (new Date()).getTime()
    },
    clickConvert() {
      this.error = null
      let input = this.input.trim()
      if (!input) {
        this.error = 'Please enter some text!'
        return
      }
      if (input.includes('THE TABLEAU')) {
        input = input.split("\n").slice(1).join("\n").trim()
      }
      const lines = input.split("\n")
      const rows = []
      lines.forEach((line) => {
        const lines = line.split(/\s+/).filter((s) => s !== '')
        const newRow = []
        for (let i = 0; i < lines.length; i++) {
          if (lines[i] === 'SLK') {
            newRow.push(lines[i] + ' ' + lines[i + 1])
            i++
          } else {
            let value = lines[i]
            if (this.convertDotIntoComma) {
              value = value.replace('.', ',')
            }
            newRow.push(value)
          }
        }
        rows.push(newRow)
      })
      exportFromJSON({
        data: rows,
        fileName: this.getFileName(),
        exportType: exportFromJSON.types.xls
      })
    }
  }
}
</script>
