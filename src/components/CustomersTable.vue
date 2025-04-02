<script setup>

const props = defineProps({
    show: Boolean,
    customers: Array
});


</script>

<template>

    <div v-if="show" class="customers-table">
        <table>
            <thead>
                <tr>
                    <th>ID</th>
                    <th>Name</th>
                    <th>Email</th>
                    <th>Phone</th>
                    <th>City</th>
                    <th>Date</th>
                </tr>
            </thead>
            <tbody>
                <tr v-for="customer in customers" :key="customer.id">
                    <td>{{ customer.id }}</td>
                    <td>{{ customer.name }}</td>
                    <td>{{ customer.email }}</td>
                    <td>{{ customer.phone || '-' }}</td>
                    <td>{{ customer.city || '-' }}</td>
                    <td>{{ customer.date ? new Date(customer.date).toLocaleDateString() : '-' }}</td>
                </tr>
                <tr v-if="customers.length === 0">
                    <td colspan="6" class="no-data">No customers found</td>
                </tr>
            </tbody>
        </table>
    </div>


</template>

<style scoped>
.customers-table {
    margin-top: 30px;
    width: 80%;
    max-width: 1000px;
    overflow-x: auto;
}

table {
    width: 100%;
    border-collapse: collapse;
    box-shadow: 0 2px 8px rgba(0, 0, 0, 0.1);
}

th,
td {
    padding: 12px 15px;
    text-align: left;
    border-bottom: 1px solid #ddd;
}

th {
    background-color: #42b983;
    color: white;
    font-weight: 500;
}

tr:hover {
    background-color: #f5f5f5;
}

.no-data {
    text-align: center;
    padding: 20px;
    color: #666;
}
</style>