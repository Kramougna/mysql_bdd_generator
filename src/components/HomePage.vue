<template>
  <div class='homepage'>
    <div class='columns'>
      <div class='column'>
        <div class='box'>
          <input v-model='database_name' placeholder='[DATA_BASE]'>
          <input v-model='collate' placeholder='[COLLATE]'>
          <input v-model='user' placeholder='[USER]'>
          <input v-model='password' placeholder='[PASSWORD]'>
          <input v-model='sql_file' placeholder='[SQL_FILE]'>
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
      database_name: '',
      password: '',
      sql_file: '',
      user: ''
    }
  },
  computed: {
    createDatabase () {
      return `CREATE DATABASE \`${this.database_name || '[DATA_BASE]'}\` COLLATE = '${this.collate || '[COLLATE]'}';`
    },
    createUser () {
      return `CREATE USER \`${this.user || '[USER]'}\`@'localhost' IDENTIFIED BY '${this.password || '[PASSWORD]'}';`
    },
    grantUser () {
      return `GRANT ALL PRIVILEGES ON \`${this.database_name || '[DATA_BASE]'}\`.* TO \`${this.user || '[USER]'}\`@'localhost';`
    },
    flushPrivileges () {
      return `FLUSH PRIVILEGES;`
    },
    importDatabase () {
      return `mysql -h localhost -u${this.user || '[USER]'} -p${this.password || '[PASSWORD]'} ${this.database_name || '[DATA_BASE]'} < ${this.sql_file || '[SQL_FILE]'}`
    },
    exportDatabase () {
      return `mysqldump -h localhost -u${this.user || '[USER]'} -p${this.password || '[PASSWORD]'} -r${this.sql_file || '[SQL_FILE]'} ${this.database_name || '[DATA_BASE]'}`
    }
  }
}
</script>
