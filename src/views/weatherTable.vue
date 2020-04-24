<template>
    <div>
        <table id="weather">
            <tr>
                <td>Wind</td>
                <td>{{weather.wind.speed }}m/s,({{weather.wind.deg}})</td>
            </tr>
            <tr>
                <td>Humidity</td>
                <td>{{weather.main.humidity}} %</td>
            </tr>
            <tr>
                <td>Pressure</td>
                <td>{{weather.main.pressure}}</td>
            </tr>
            <tr>
                <td>Latitude</td>
                <td>{{weather.coord.lat}}</td>
            </tr>
            <tr>
                <td>Longitude</td>
                <td>{{weather.coord.lon}}</td>
            </tr>

        </table>
    </div>
</template>
<script>
    export default {
        props:['weather']
    }

</script>
<style>

</style>
