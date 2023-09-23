<template>
    <div>
        <h2>List of Employees and Sales Data</h2>
        <ul>
            <li v-for="employee in employees" :key="employee.id">
                <h3>{{ employee.name }}</h3>
                <p>Email: {{ employee.email }}</p>
                <p>Total Sales: {{ calculateTotalSales(employee.sales) }}</p>
            </li>
        </ul>
        <h2>Employee with Highest Total Sales</h2>
        <p>Name: {{ employeeWithHighestSales.name }}</p>
        <p>Email: {{ employeeWithHighestSales.email }}</p>
        <p>Total Sales: {{ calculateTotalSales(employeeWithHighestSales.sales) }}</p>
    </div>
</template>
  
<script setup>
import { ref, onMounted, computed } from 'vue';

const employees = ref([
    {
        id: 1,
        name: 'John',
        email: 'john3@example.com',
        sales: [
            { customer: 'The Blue Rabbit Company', order_total: 7444 },
            { customer: 'Black Melon', order_total: 1445 },
            { customer: 'Foggy Toaster', order_total: 700 }
        ]
    },
    {
        id: 2,
        name: 'Jane',
        email: 'jane8@example.com',
        sales: [
            { customer: 'The Grey Apple Company', order_total: 203 },
            { customer: 'Yellow Cake', order_total: 8730 },
            { customer: 'The Piping Bull Company', order_total: 3337 },
            { customer: 'The Cloudy Dog Company', order_total: 5310 }
        ]
    },
    {
        id: 3,
        name: 'Dave',
        email: 'dave1@example.com',
        sales: [
            { customer: 'The Acute Toaster Company', order_total: 1091 },
            { customer: 'Green Mobile', order_total: 2370 }
        ]
    }
]);

const calculateTotalSales = (sales) => {
    if (!Array.isArray(sales)) {
        return 0;
    }
    return sales.reduce((total, sale) => total + sale.order_total, 0);
};

const employeeWithHighestSales = computed(() => {
    return employees.value.reduce((prev, current) => {
        const prevTotal = calculateTotalSales(prev.sales);
        const currentTotal = calculateTotalSales(current.sales);
        return prevTotal > currentTotal ? prev : current;
    }, {});
});
</script>

<style>
    ul li {
        list-style: none;
    }
</style>