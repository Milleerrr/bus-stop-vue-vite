<script setup>
import { ref } from 'vue'
import BusStop from './BusStop.vue';

let peopleWaiting = ref(null);
let capacity = ref(null);
let passengers = ref(null);

// Bus methods to retrieve information about the Bus object
const getSeatsAvailable = () => {
    return capacity.value - passengers.value;
}

const setBusCapcity = (e) => {
    capacity.value = parseInt(e.target.value);
}

const setPassengers = (e) => {
    passengers.value = parseInt(e.target.value);
};

// Method to update peopleWaiting when BusStop informs of a change
const updatePeopleWaiting = (newValue) => {
  peopleWaiting.value = newValue;
};

// Method to calculate how many people can get on the bus
const peopleGettingOnBus = () => {
    const seatsAvailable = getSeatsAvailable();

    if (peopleWaiting <= seatsAvailable) {
        passengers.value += peopleWaiting;
        peopleWaiting.value -= peopleWaiting;
    } else {
        passengers.value += seatsAvailable;
        peopleWaiting.value -= seatsAvailable;
    };
};

const busAlertMessage = () => {
    return `Bus details:
                Capcity: ${capacity.value} 
                People on bus: ${passengers.value}
                Seats free: ${getSeatsAvailable()}.
                People waiting at the bus stop ${peopleWaiting.value}`;
};

// Initiate bus start up sequence
const initiateBusSequence = () => {

    // Bus arrives at first stop
    alert(`Bus arrives:
        ${busAlertMessage()}`);

    // People getting on the bus
    peopleGettingOnBus();

    // Bus leaving 
    alert(`Bus departs:
        ${busAlertMessage()}`);
};

</script>

<template>
    <form id="bus-form">
        <label for="busCapcity">Bus Capacity</label>
        <input id="busCapcity" @change="setBusCapcity($event)" placeholder="0" :value="capacity" type="number" min="0" max="50">

        <label for="seatsFree">Passengers</label>
        <input id="seatsFree" @change="setPassengers($event)" placeholder="0" :value="passengers" type="number" min="0" max="50">

        <BusStop :peopleWaiting="peopleWaiting" @update:peopleWaiting="updatePeopleWaiting" />

        <button id="start-sequence" @click.prevent="initiateBusSequence">Start Bus Sequence</button>
    </form>
</template>

  

<style scoped>

#bus-form {
    display: flex;
    flex-direction: column;
    border: 1px solid white;
    border-radius: 10px;
    padding: 10px
}

#start-sequence {
    margin-top: 10px;
}

</style>
