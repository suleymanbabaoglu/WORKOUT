<template>
  <div>
    <b-button class="mb-3" variant="primary" @click="create">CREATE</b-button>
    <b-table striped hover :items="items" :fields="fields">
      <template #cell(password)="data">
        <b-icon-key-fill
          font-scale="2"
          role="button"
          @click="passwordReset(data.item.id)"
        />
      </template>
      <template #cell(actions)="data">
        <b-icon-pen-fill
          class="mr-3"
          role="button"
          @click="update(data.item.id)"
        />
        <b-icon-trash-fill role="button" @click="deleteUser(data.item.id)" />
      </template>
    </b-table>
    <b-modal
      centered
      v-model="modalComponent.visible"
      no-close-on-backdrop
      no-close-on-esc
      busy
    >
      <component
        :is="modalComponent.component"
        v-bind="modalComponent.props"
        @closeModal="closeModal"
      />
      <template #modal-footer>
        <div></div>
      </template>
    </b-modal>
  </div>
</template>

<script>
import BaseActions from "../../store/BaseActions";
import { ControllerRoutes } from "../../constraints/Routes";
import PasswordReset from "../../components/User/PasswordReset";
import CreateUpdateForm from "../../components/User/CreateUpdateForm";

export default {
  data() {
    return {
      fields: [
        { key: "id" },
        { key: "firstName", label: "First Name" },
        { key: "lastName", label: "Last Name" },
        { key: "email", label: "E-Mail" },
        { key: "password", label: "Password" },
        { key: "actions", label: "Actions" }
      ],
      items: [],
      modalComponent: {
        visible: false,
        component: null,
        props: []
      }
    };
  },
  created() {
    this.initialize();
  },
  methods: {
    async initialize() {
      this.items = await new BaseActions(ControllerRoutes.User).getAll();
    },
    create() {
      this.modalComponent = {
        visible: true,
        props: { create: true },
        component: CreateUpdateForm
      };
    },
    update(userId) {
      this.modalComponent = {
        visible: true,
        props: { create: false, userId: userId },
        component: CreateUpdateForm
      };
    },
    async deleteUser(userId) {
      await new BaseActions(ControllerRoutes.User).delete(userId);
      this.items.splice(
        this.items.indexOf(this.items.find(u => u.id === userId)),
        1
      );
    },
    passwordReset(userId) {
      this.modalComponent = {
        visible: true,
        props: { userId: userId },
        component: PasswordReset
      };
    },
    closeModal() {
      this.modalComponent.visible = false;
      this.initialize();
    }
  }
};
</script>
