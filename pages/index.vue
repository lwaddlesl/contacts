<template>
  <v-main>
    <v-container>
      <div>
        <h1>Add contacts</h1>
      </div>

      <v-text-field
        label="Input phone"
        hide-details="auto"
        clearable
        v-model="newNumber"
      ></v-text-field>
      <v-text-field
        label="input name"
        hide-details="auto"
        clearable
        v-model="newName"
      >
      </v-text-field>

      <div class="text-right ma-3">
        <v-btn @click="add" class="text-center" fab dark color="indigo">
          <v-icon dark> mdi-plus </v-icon>
        </v-btn>
      </div>

      <v-list flat two-line>
        <div v-for="contact in contacts" :key="contact.id">
          <v-list-item>
            <template>
              <v-list-item-content>
                <v-list-item-title>{{ contact.title }}</v-list-item-title>
                <v-list-item-subtitle>
                  {{ contact.subTitle }}
                </v-list-item-subtitle>
              </v-list-item-content>
              <v-list-item-action>
                <v-btn @click="deleteContacts(contact.id)" icon>
                  <v-icon color="grey lighten-1">mdi-delete</v-icon>
                </v-btn>
              </v-list-item-action>
              <v-dialog v-model="dialog" max-width="500px">
                <template v-slot:activator="{ on }">
                  <v-btn @click="changeContacts(contact.id)" v-on="on" icon>
                    <v-icon color="grey lighten-1">mdi-lead-pencil</v-icon>
                  </v-btn>
                </template>
                <v-card>
                  <v-card-title>Change info</v-card-title>
                  <v-card-text>
                    <v-text-field
                      v-model="changed.title"
                      label="Input phone"
                    ></v-text-field>
                    <v-text-field
                      v-model="changed.subTitle"
                      label="Input name"
                    ></v-text-field>
                  </v-card-text>

                  <v-card-actions>
                    <v-spacer></v-spacer>

                    <v-btn text color="primary" @click="dialog = false">
                      Submit
                    </v-btn>
                  </v-card-actions>
                </v-card>
              </v-dialog>
            </template>
          </v-list-item>
          <v-divider> </v-divider>
        </div>
      </v-list>
    </v-container>
  </v-main>
</template>
<script>
export default {
  data: () => ({
    newNumber: "",
    newName: "",
    changed: [],
    dialog: false,
    contacts: [
      {
        id: 1,
        title: "891432423423",
        subTitle: "Nik",
      },
      {
        id: 2,
        title: "89123432424",
        subTitle: "Kate",
      },
      {
        id: 3,
        title: "891234324234",
        subTitle: "Ann",
      },
    ],
  }),
  methods: {
    // submitChanges() {
    //   this.contacts = this.contacts.filter(
    //     (contact) => contact.id !== this.changed.id
    //   );
    //   this.contacts.push(this.changed);
    //   this.dialog = false;
    //   this.changed = "";
    // },
    changeContacts(id) {
      this.changed = this.contacts.filter((contact) => contact.id === id)[0];
    },
    deleteContacts(id) {
      this.contacts = this.contacts.filter((contact) => contact.id !== id);
    },
    add() {
      if (this.newContacts != "" && this.newName != "") {
        let newContacts = {
          id: Date.now(),
          title: this.newNumber,
          subTitle: this.newName,
        };
        this.contacts.push(newContacts);
        this.newNumber = "";
        this.newName = "";
      }
    },
  },
};
</script>