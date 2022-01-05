<template>
    <div>
        <FilterTransfer />
        <Tabs
            @click-tickets-low-cost="onClickLowCost"
        />
        <Tickets />
    </div>

</template>

<script>
import FilterTransfer from '../components/FilterTransfer.vue'
import Tabs from '../components/Tabs.vue'
import Tickets from '../components/Tickets.vue'

import { getTicketsUrl } from '../constants.js';

export default {
    components: {
        FilterTransfer,
        Tabs,
        Tickets,
    },
    data() {
        return {
            searchId: '',
            tickets: [],
        };
    },
    async created () {
        await this.getSearchId();
        await this.getTickets();
    },
    methods: {
        async getSearchId() {
            const responseSearchId = await fetch('https://front-test.beta.aviasales.ru/search'); // {"searchId":"4niyd"}
            const { searchId } = await responseSearchId.json(); // { searchId: "4niyd" }
            this.searchId = searchId;
        },
        async getTickets() {
            const responseTickets = await fetch(`${getTicketsUrl}?searchId=${this.searchId}`);
            const { tickets, stop } = await responseTickets.json();
            console.log(tickets);
            if( stop ) {
                return;
            }
            this.tickets = tickets;
        },
        onClickLowCost() {
            this.tickets.sort()
        }
    }
}

</script>