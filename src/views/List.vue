<template>
  <div>
    <input type="text" v-model="newContact" placeholder="Name" />
    <button @click="addContact">Add Contact</button>
    <button @click="sortContacts">Sort</button>

    <!-- use named transition "slide-up" -->
    <!-- tag shows how to render the transition-group wrapper of this multiple elements (default is span)  -->
    <!-- appear attribute tell the transition-group that not only do we want the slide-up transition to happen every time a new member of the group is added, but also when the entire group (the entire ul) is first rendered -->
    <transition-group name="slide-up" tag="ul" appear>
      <li v-for="contact in contacts" :key="contact">
        {{ contact }}
      </li>
    </transition-group>
  </div>
</template>

<script>
export default {
  data() {
    return {
      newContact: '',
      contacts: ['Beau Thabeast', 'Cindy Rella', 'Alice Vunderlind']
    }
  },
  methods: {
    addContact() {
      this.contacts.push(this.newContact)
      this.newContact = ''
    },
    sortContacts() {
      this.contacts.sort()
    }
  }
}
</script>
