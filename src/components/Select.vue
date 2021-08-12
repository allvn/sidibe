<template>
  <div>
    <!-----------Selection Simple--------------->
    <select v-if="type == 'simple'" v-model="select">
      <option v-for="(item, i) in liste" :key="i" :value="item.name">
        {{ item.name }}
      </option>
    </select>
    <!-----------Selection Multiple--------------->
    <select v-if="type == 'multiple'" v-model="select" multiple>
      <option v-for="(item, i) in liste" :key="i" :value="item.name">
        {{ item.name }}
      </option> 
    </select>
    <!-----------Selection Guidée--------------->
    <div class="guide_parent" v-if="type == 'guide'">
      <input
        type="search"
        placeholder="Search"
        v-model="text"
        @click="show = !show"
        @keyup="Search"
      />
      <div class="guide" v-show="show">
        <p v-for="(item, i) in searchList" :key="i" @click="Close(item)">
          {{ item.name }}
        </p>
      </div>
    </div>

    <p>{{ select }}</p>
  </div>
</template>

<script>
export default {
  props: ["liste", "type"],
  data() {
    return {
      select: "",
      show: false,
      text: "",
      searchList: [],
    };
  },
  methods: {
    Search() {
      this.show = true;
      var results = [];
      this.liste.forEach((item) => {
        if (item.name.includes(this.text)) results.push(item);
      });

      this.searchList = results;

      console.log(results);
    },

    Close(item){
      this.select = item.name
      this.show = false
    },
  },

  mounted() {
    this.searchList = this.liste;
  },
};
</script>

<style lang="css" scoped>
select {
  padding: 20px 40px;
  font-size: 18px;
}

.guide_parent {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

input {
  padding: 8px 16px;
  margin: 4px 0;
  width: 50%;
  border-radius: 15px;
}

.guide {
  background-color: #fff;
  border: 1px solid #000;
  width: 50%;
  padding: 0.5rem 0;
}

p {
  text-align: left !important;
  padding: 0.375rem 1rem;
  margin: 0;
  font-size: 0.875rem;
  line-height: 1.5;
  cursor: pointer;
  color: #0a0a0a;
}

p:hover {
  background-color: #f5f5f5;
}
</style>
