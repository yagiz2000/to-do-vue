<template>
  <div id="searchBar">
    <form v-on:submit.prevent>
      <div class="form-group d-flex justify-content-center ">
        <div class="row text-center d-flex " style="max-width:1048px">
          <div class="col">
            <label for="toDo"
              ><big
                style="font-family:-apple-system, BlinkMacSystemFont, sans-serif;font-weight: bold; font-size:250%"
                >Yapman Gereken İş</big
              ></label
            >
            <input
              v-model="message"
              type="text"
              class="form-control mt-2"
              id="toDo"
              placeholder="Todonuzu giriniz"
              ref="inputText"
            />
            <button
              v-on:click="handleMessage"
              type="submit"
              class="btn btn-success mt-2"
            >
              Ekle
            </button>
          </div>
        </div>
      </div>
    </form>
  </div>
</template>

<script>
export default {
  name: "SearchBar",
  data() {
    return {
      message: "",
    };
  },
  methods: {
    handleMessage() {
      this.$emit("messageString", this.message);
      this.$refs.inputText.value = "";
      this.message = "";
    },
  },
};
</script>

<style></style>
