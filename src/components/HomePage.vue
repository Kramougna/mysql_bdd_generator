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
          <div class='columns'>
            <div class='column'>
              <strong>CREATE DATABASE :</strong>
              <p>{{createDatabase}}</p>
            </div>

            <div class='column is-2'>
              <button type='button' v-clipboard:copy='createDatabase'>Copy create db</button>
            </div>
          </div>

          <div class='columns'>
            <div class='column'>
              <strong>CREATE USER :</strong>
              <p>{{createUser}}</p>
            </div>

            <div class='column is-2'>
              <button type='button' v-clipboard:copy='createUser'>Copy create user</button>
            </div>
          </div>

          <div class='columns'>
            <div class='column'>
              <strong>GRANT ALL PRIVILEGES :</strong>
              <p>{{grantUser}}</p>
            </div>

            <div class='column is-2'>
              <button type='button' v-clipboard:copy='grantUser'>Copy grant user</button>
            </div>
          </div>

          <div class='columns'>
            <div class='column'>
              <strong>FLUSH PRIVILEGES :</strong>
              <p>{{flushPrivileges}}</p>
            </div>

            <div class='column is-2'>
              <button type='button' v-clipboard:copy='flushPrivileges'>Copy flush</button>
            </div>
          </div>
        </div>
      </div>

      <div class='column'>
        <div class='box'>
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
      </div>
    </div>
  </div>
</template>

<script>
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
    createDatabase () {
      /* #TODO. refacto || in computed */
      return `CREATE DATABASE \`${this.dataBaseValue}\` COLLATE = '${this.collateValue}';`
    },
    createUser () {
      /* #TODO. refacto || in computed */
      return `CREATE USER \`${this.userValue}' IDENTIFIED BY '${this.passwordValue}';`
    },
    grantUser () {
      /* #TODO. refacto || in computed */
      return `GRANT ALL PRIVILEGES ON \`${this.dataBaseValue}\`.* TO \`${this.userValue}\`@'${this.hostValue}';`
    },
    flushPrivileges () {
      return 'FLUSH PRIVILEGES;'
    },
    importDatabase () {
      /* #TODO. refacto || in computed */
      return `mysql -h ${this.hostValue} -u${this.userValue} -p'${this.passwordValue}' ${this.dataBaseValue} < ${this.sqlFileValue}`
    },
    exportDatabase () {
      /* #TODO. refacto || in computed */
      return `mysqldump -h ${this.hostValue} -u${this.userValue} -p'${this.passwordValue}' -r${this.sqlFileValue} ${this.dataBaseValue}`
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
      return this.host || '[COLLATE]'
    },
    sqlFileValue () {
      return this.sqlFile || '[SQL_FILE]'
    }
  }
}
</script>
