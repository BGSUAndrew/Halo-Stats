<template>
    <div class="header">
        <div>
            <h1>SERVICE RECORD</h1>
            <p>Gamertag: AO1793</p>
            <p>Clan: XG</p>
            <p>Time spent playing: {{info.time_played.human}}</p>
        </div>
        <div>
            <img class="emblem" src="./icons/emblem.png" alt="emblem">
        </div>
    </div>

    <div class="stats">
        <p class="heading">SUMMARY</p>
            <div class="stats_grid">
                <div class="stats_item">
                    <p class="sub-heading">Total Kills:</p>
                    <p class="stat-number">{{info.core.summary.kills}}</p>
                </div>
                <div class="stats_item">
                    <p class="sub-heading">Total Deaths:</p>
                    <p class="stat-number">{{info.core.summary.deaths}}</p>
                </div>
                <div class="stats_item">
                    <p class="sub-heading">Total Assists:</p>
                    <p class="stat-number">{{info.core.summary.assists}}</p>
                </div>
                 <div class="stats_item">
                    <p class="sub-heading">Total KDR:</p>
                    <p class="stat-number">{{info.core.kdr}}</p>
                </div>
                <div class="stats_item">
                    <p class="sub-heading">Total KDA:</p>
                    <p class="stat-number">{{info.core.kda}}</p>
                </div>
            </div>
        <p class="heading">KILL BREAKDOWN</p>
        <div class="stats_grid">
            <div class="stats_item">
                <p class="sub-heading">Melee Kills:</p>
                <p class="stat-number">{{info.core.breakdowns.kills.melee}}</p>
            </div>
            <div class="stats_item">
                <p class="sub-heading">Grenade Kills:</p>
                <p class="stat-number">{{info.core.breakdowns.kills.grenades}}</p>
            </div>
            <div class="stats_item">
                <p class="sub-heading">Headshot Kills:</p>
                <p class="stat-number">{{info.core.breakdowns.kills.headshots}}</p>
            </div>
            <div class="stats_item">
                <p class="sub-heading">Power Weapon Kills:</p>
                <p class="stat-number">{{info.core.breakdowns.kills.power_weapons}}</p>
            </div>
            <div class="stats_item">
                <p class="sub-heading">Accuracy:</p>
                <p class="stat-number">{{info.core.shots.accuracy}}</p>
            </div>
        </div>
    <p class="heading">WINS AND LOSSES</p>
    <div class="stats_grid">
        <div class="stats_item">
            <p class="sub-heading">Matches Played:</p>
            <p class="stat-number">{{info.matches_played}}</p>
        </div>
        <div class="stats_item">
            <p class="sub-heading">Matches Won:</p>
            <p class="stat-number">{{info.core.breakdowns.matches.wins}}</p>
        </div>
        <div class="stats_item">
            <p class="sub-heading">Matches Lost:</p>
            <p class="stat-number">{{info.core.breakdowns.matches.losses}}</p>
        </div>
        <div class="stats_item">
            <p class="sub-heading">Matches Left Early (shame stat):</p>
            <p class="stat-number">{{info.core.breakdowns.matches.left}}</p>
        </div>
        <div class="stats_item">
            <p class="sub-heading">Win Rate:</p>
            <p class="stat-number">{{info.win_rate}}</p>
        </div>
    </div>
    <p style="text-align:center;">This project is maintained by Andrew O'Connor. The stats are provided by HaloDotAPI and images are provided by 343i.</p>

</div>

</template>


<script>
    export default {
        data() {
            return {
                info: null
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
            .then(response => (this.info = response.data))
            .then(result => console.log(result.data))
        }
    }
</script>



<style scoped>
h1,p {
    color: #fff;
}

p {
    margin-bottom: 0px;
    margin-top: 5px;
}

.header {
    display: flex;
    justify-content: space-between;
}

.stats {
    margin-top: 2rem;
    background-color: #00000045;
}

.stats_grid {
    display: grid;
    grid-template-columns: 1fr 1fr 1fr 1fr 1fr;
}

.heading {
    font-size: 2rem;
    margin-bottom: 0px;
    margin-top: 20px;
    padding: 0.5rem;
}

.sub-heading{
    font-size: 1.75rem;
    margin-bottom: 0px;
    margin-top: 5px;
    text-align: center;
    padding: 0.5rem
}

.stat-number {
    font-size: 1.5rem;
    text-align: center;
    margin-top: 0px;
}

.emblem {
    max-width: 200px;
    width: 100%;
    height: auto;
}

@media (max-width:700px) {
    .stats_grid {
        display: block;
    }
}

</style>
