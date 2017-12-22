<template>
  <div class='data-base-command'>
    <div class='columns'>
      <div class='column'>
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
  </div>
</template>

<script>
export default {
  name: 'DataBaseCommand',
  props: ['dataBaseConfig'],
  computed: {
    createDatabase () {
      /* #TODO. refacto || in computed */
      return `CREATE DATABASE \`${this.dataBaseConfig.databaseName}\` COLLATE = '${this.dataBaseConfig.collate}';`
    },
    createUser () {
      /* #TODO. refacto || in computed */
      return `CREATE USER '${this.dataBaseConfig.user}'@'${this.dataBaseConfig.host}' IDENTIFIED BY '${this.dataBaseConfig.password}';`
    },
    grantUser () {
      /* #TODO. refacto || in computed */
      return `GRANT ALL PRIVILEGES ON \`${this.dataBaseConfig.databaseName}\`.* TO \`${this.dataBaseConfig.user}\`@'${this.dataBaseConfig.host}';`
    },
    flushPrivileges () {
      return 'FLUSH PRIVILEGES;'
    }
  }
}
</script>
