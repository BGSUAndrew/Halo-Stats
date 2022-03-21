<template>
    <div class="stats">
        <p class="heading">KILLS BREAKDOWN</p>
        <div class="stats_grid">
            <div class="stats_item">
                <p class="sub-heading">Melee Kills:</p>
                <p class="stat-number">{{info.data.core.breakdown.kills.melee}}</p>
            </div>
            <div class="stats_item">
                <p class="sub-heading">Grenades Kills:</p>
                <p class="stat-number">{{info.data.core.breakdown.kills.grenades}}</p>
            </div>
            <div class="stats_item">
                <p class="sub-heading">Headshot Kills:</p>
                <p class="stat-number">{{info.data.core.breakdowns.kills.headshots}}</p>
            </div>
            <div class="stats_item">
                <p class="sub-heading">Power Weapon Kills:</p>
                <p class="stat-number">{{info.data.core.breakdowns.kills.power_weapons}}</p>
            </div>
        </div>
</div>

</template>


<script>
    export default {
        data() {
            return {
                info: []
            }
        }, 
        mounted() {
            const dataHeader = new Headers();

            dataHeader.append('Authorization','Bearer tok_dev_pCxjr1PZNmBbHCnhQmRaJwmkax5QDNFLuqJdYXsYUE3LAgGohB3QbBZgcCZghsJn');

            const requestOptions = {
                method: 'GET',
                headers: dataHeader,
                redirect: 'follow'
            };

            fetch('https://halo.api.stdlib.com/infinite@0.3.9/stats/service-record/multiplayer/?filter=matchmade:pvp&gamertag=AO1793', requestOptions)
            .then(response => response.json())
            .then(info => this.info = info)
        }
    }
</script>



<style scoped>
h1,p {
    color: #fff;
}

.stats_grid {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr 1fr;
}

.heading {
    font-size: 2rem;
    margin-bottom: 0px;
}

.sub-heading{
    font-size: 1.75rem;
    margin-bottom: 0px;
    text-align: center;
}

.stat-number {
    font-size: 1.5rem;
    text-align: center;
    margin-top: 0px;
}

</style>
