<template>
  <div>
    <h2 class="text-center my-4">Danh sách học sinh của năm</h2>
    <student-btn :edit="hocsinh" @submit="clickAdd" />
    <table class="table text-center">
      <thead>
        <tr>
          <th>ID</th>
          <th class="text-left">Name</th>
          <th>Age</th>
          <th>Phone</th>
          <th class="text-left">Address</th>
          <th>Action</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="item in list" :key="item.id">
          <th>{{ item.id }}</th>
          <th class="text-left">{{ item.name }}</th>
          <th>{{ item.age }}</th>
          <th>{{ item.phone }}</th>
          <th class="text-left">{{ item.address }}</th>
          <th>
            <button v-b-modal.modal-prevent-closing @click="clickEdit(item)">
              Edit
            </button>
            <button @click="clickDelete(item)">Delete</button>
          </th>
        </tr>
      </tbody>
    </table>
  </div>
</template>

<script>
import StudentBtn from './StudentBtn.vue'
export default {
  components: { StudentBtn },

  data() {
    return {
      hocsinh: {},
      list: [
        {
          id: 1,
          name: 'Nguyen Thanh Chung',
          age: 20,
          phone: 387133658,
          address: 'Hai Duong',
        },
        {
          id: 2,
          name: 'Nguyen Thuy Linh',
          age: 19,
          phone: 387284738,
          address: 'Ha Noi',
        },
        {
          id: 3,
          name: 'Tran Thi Bich Hanh',
          age: 21,
          phone: 3871345434,
          address: 'Thanh Hoa',
        },
        {
          id: 4,
          name: 'Lo Luu Dan',
          age: 30,
          phone: 3583843658,
          address: 'Vung Nui',
        },
      ],
    }
  },

  methods: {
    clickAdd(item) {
      const index = this.list.findIndex((c) => c.id === item.id)
      if (index >= 0) {
        this.list.splice(index, 1, item)
      } else {
        this.list.push(item)
      }
    },

    clickDelete(itemDelete) {
      for (let i = 0; i < this.list.length; i++) {
        if (itemDelete.id === this.list[i].id) {
          this.list.splice(i, 1)
        }
      }
    },

    clickEdit(itemEdit) {
      this.hocsinh = itemEdit
    },
  },
}
</script>

<style></style>
