<template>
  <Window title="weatherornot" width="400" height="100" margined v-on:close="exit">
    <Box padded>
      <Text>Welcome to your Vuido application!</Text>
      <Box padded>
        <Form padded>
          <Text>
            Add a new name
          </Text>
          <TextInput label="First name:" v-model="firstName"/>
          <TextInput label="Last name:" v-model="lastName"/>
        </Form>
        <Button @click="addName">Add</Button>
        <Text>
          You're name is:
          {{ fullName }}
        </Text>
        <Box>
          <Text>
            Names:
          </Text>
          <Text v-for="name in names">
            {{ name }}
          </Text>
        </Box>
        <Button v-if="names.length" @click="openOther(names[0])">Open</Button>
      </Box>
    </Box>
  </Window>
</template>

<script>
import Vue from 'vuido';
import OtherWindow from './OtherWindow';

export default {
  data() {
    return {
      names: [],
      firstName: '',
      lastName: '',
      otherWindows: []
    }
  },
  components: {
    OtherWindow
  },
  computed: {
    fullName() {
      return `${this.firstName} ${this.lastName}`
    }
  },
  methods: {
    exit() {
      this.$exit();
    },
    addName() {
      this.names.push(this.fullName);
      this.firstName = '';
      this.lastName = '';
    },
    openOther(nameArg) {
      let new_other = new Vue( {

        render: h => h( OtherWindow,
          {
            props: {
            userName: nameArg
          }
          }
        )
      });

      new_other.$mount()
    }
  }
}
</script>
