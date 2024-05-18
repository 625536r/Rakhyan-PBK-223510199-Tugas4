<template>
  <div>
    <h2>Form Pembelanjaan</h2>
    <form @submit.prevent="submitForm" class="expense-form">
      <div class="form-group">
        <label for="description">Nama Barang</label>
        <input type="text" v-model="description" class="form-control" placeholder="Masukkan nama barang">
      </div>
      <div class="form-group">
        <label for="price">Harga Barang</label>
        <input type="number" v-model.number="price" class="form-control" placeholder="Masukkan harga barang">
      </div>
      <div class="form-group">
        <label for="quantity">Jumlah Barang</label>
        <input type="number" v-model.number="quantity" class="form-control" placeholder="Masukkan jumlah barang">
      </div>
      <button type="submit" class="btn">Tambah Pembelanjaan</button>
    </form>
  </div>
</template>

<script>
export default {
  name: 'ExpenseForm',
  data() {
    return {
      description: '',
      price: '',
      quantity: ''
    };
  },
  methods: {
    submitForm() {
      const total = this.price * this.quantity;
      const expense = {
        description: this.description,
        price: this.price,
        quantity: this.quantity,
        total: total
      };
      this.$emit('add-expense', expense);
      this.clearForm();
    },
    clearForm() {
      this.description = '';
      this.price = 0;
      this.quantity = 1;
    }
  }
}
</script>

<style scoped>
.expense-form {
  display: flex;
  flex-direction: column;
  gap: 10px;
}

.form-group {
  display: flex;
  flex-direction: column;
}

label {
  margin-bottom: 5px;
}

.form-control {
  padding: 5px;
  border: 1px solid #ccc;
  border-radius: 3px;
}

.btn {
  background-color: #3498db;
  color: white;
  border: none;
  padding: 10px 20px;
  cursor: pointer;
}

.btn:hover {
  background-color: #2980b9;
}
</style>
