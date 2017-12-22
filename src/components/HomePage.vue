<template>
  <div class='homepage'>
    <div class='columns'>
      <div class='column'>
        <div class='box'>
          <input v-model='databaseName' placeholder='[DATA_BASE]'>
          <input v-model='collate' placeholder='[COLLATE]'>
          <input v-model='user' placeholder='[USER]'>
          <input v-model='host' placeholder='[HOST]'>
          <input v-model='password' placeholder='[PASSWORD]'>
          <input v-model='sqlFile' placeholder='[SQL_FILE]'>
        </div>
      </div>
    </div>

    <div class='columns'>
      <div class='column'>
        <div class='box'>
          <data-base-command :data-base-config='dataBaseConfig'></data-base-command>
        </div>
      </div>

      <div class='column'>
        <div class='box'>
          <data-base-transfer :transfer-config='transferConfig'></data-base-transfer>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import DataBaseCommand from '@/components/DataBaseCommand'
import DataBaseTransfer from '@/components/DataBaseTransfer'

export default {
  name: 'HomePage',
  data () {
    return {
      collate: 'utf8_general_ci',
      databaseName: '',
      host: 'localhost',
      password: '',
      sqlFile: '',
      user: ''
    }
  },
  computed: {
    baseConfig () {
      return {
        databaseName: this.dataBaseValue,
        host: this.hostValue,
        password: this.passwordValue,
        user: this.userValue
      }
    },
    dataBaseConfig () {
      return Object.assign({}, this.baseConfig, { collate: this.collateValue })
    },
    transferConfig () {
      return Object.assign({}, this.baseConfig, { sqlFile: this.sqlFileValue })
    },
    dataBaseValue () {
      return this.databaseName || '[DATA_BASE]'
    },
    userValue () {
      return this.user || '[USER]'
    },
    passwordValue () {
      return this.password || '[PASSWORD]'
    },
    hostValue () {
      return this.host || '[HOST]'
    },
    collateValue () {
      return this.collate || '[COLLATE]'
    },
    sqlFileValue () {
      return this.sqlFile || '[SQL_FILE]'
    }
  },
  components: {
    DataBaseCommand,
    DataBaseTransfer
  }
}
</script>
