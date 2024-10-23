<template>
  <div class="page">
    <h4>Thêm Liên hệ Mới</h4>
    <ContactForm :contact="newContact" @submit:contact="addContact" />
    <p>{{ message }}</p>
  </div>
</template>

<script>
import ContactForm from "@/components/ContactForm.vue";
import ContactService from "@/services/contact.service";

export default {
  components: {
    ContactForm,
  },
  data() {
    return {
      newContact: {
        name: "",
        email: "",
        address: "",
        phone: "",
        favorite: false,
      },
      message: "",
    };
  },
  methods: {
    async addContact(data) {
      try {
        await ContactService.create(data); // Gọi dịch vụ để thêm liên hệ mới
        alert("Liên hệ được thêm thành công.");
        this.$router.push({ name: "contactbook" }); // Chuyển hướng về danh sách liên hệ
      } catch (error) {
        console.log(error);
        this.message = "Đã xảy ra lỗi khi thêm liên hệ.";
      }
    },
  },
};
</script>

<style scoped>
@import "@/assets/form.css"; /* Nếu có style riêng cho form */
</style>
