<template>
  <div class='data-base-transfer'>
    <div class='columns'>
      <div class='column'>
        <strong>Import BDD</strong>
        <p>{{importDatabase}}</p>
      </div>

      <div class='column is-2'>
        <button type='button' v-clipboard:copy='importDatabase'>Copy Import</button>
      </div>
    </div>

    <div class='columns'>
      <div class='column'>
        <strong>Export BDD</strong>
        <p>{{exportDatabase}}</p>
      </div>

      <div class='column is-2'>
        <button type='button' v-clipboard:copy='exportDatabase'>Copy Export</button>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'DataBaseTransfer',
  props: ['transferConfig'],
  computed: {
    importDatabase () {
      /* #TODO. refacto || in computed */
      return `mysql -h ${this.transferConfig.host} -u${this.transferConfig.user} -p'${this.transferConfig.password}' ${this.transferConfig.databaseName} < ${this.transferConfig.sqlFile}`
    },
    exportDatabase () {
      /* #TODO. refacto || in computed */
      return `mysqldump -h ${this.transferConfig.host} -u${this.transferConfig.user} -p'${this.transferConfig.password}' -r${this.transferConfig.sqlFile} ${this.transferConfig.databaseName}`
    }
  }
}
</script>
