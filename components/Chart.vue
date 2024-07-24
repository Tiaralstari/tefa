<template>
    <div>
        <canvas id="myChart"></canvas>
    </div>
</template>

<script setup>
import Chart from 'chart.js/auto'

const labels = [
    'januari',
    'february',
    'march',
    'april',
    'may',
    'june',
];

const data ={
    labels: labels,
    datasets: [{
    label: 'My First dataset',
    backgroundColor: 'rgb(220,220,220)',
    borderColor: 'rgb(2555,99,135)',
    data: [10,20,25,20,20,45,0],
    }]
};

const config = {
    type: 'bar',
    data: data,
    options: {}
};
onMounted(() => {
    const myChart = new Chart(
        document.getElementById('myChart'),
        config
    );
})
</script>

