<template>
  <section class="wrapper">
    <svg width="500" height="500">
        <defs>
            <radialGradient id="starGradient">
                <stop offset="2%" stop-color="white" />
                <stop offset="95%" :stop-color="starColour" />
            </radialGradient>
        </defs>
        <rect width="100%" height="100%" fill="#111" />
        <path
            class="radial"
            :d="radialData"
            transform="translate(250, 250)"
            fill="url(#starGradient)">
        </path>
    </svg>
    <aside>
        <div class="range-input">
            <label for="rays">Rays:</label>
            <input name="rays" type="range" min="4" max="60" v-model="rays" />
        </div>
        <div class="range-input">
            <label for="radius">Radius:</label>
            <input name="radius" type="range" min="10" max="1000" v-model="radius" />
        </div>
        <div class="range-input">
            <label for="heat">Heat</label>
            <input name="heat" type="range" min="0" max="100" v-model="heat" />
        </div>
    </aside>
  </section>
</template>


<script>
import { lineRadial } from 'd3-shape';
import { scaleLinear } from 'd3-scale';
    export default {
        name: 'Chart',

        data() {
            return {
                radius: 500,
                rays: 8,
                heat: 5
            }
        },

        computed: {
            outerRadius() {
                const scale = scaleLinear()
                    .domain([10, 1000])
                    .range([5, 250]);

                return scale(this.radius)
            },
            innerRadius() {
                return this.outerRadius * 0.5 
            },
            radialPoints() {
                const step = 2 * Math.PI / (this.rays * 2)
                const points = [];
                for (let i = 0; i <= this.rays * 2; i++) {
                    const currentRadius = i % 2 ? this.innerRadius : this.outerRadius;
                    points.push([i * step, currentRadius])
                }
                return points;
            },
            radialData() {
                const radialLineGenerator = lineRadial()
                return radialLineGenerator(this.radialPoints);
            },
            starColour() {
                const myColour = scaleLinear()
                    .domain([0, 25, 50, 75, 100])
                    .range(['#ff7665', '#ffb469', '#ffe876', '#fff', '#99cdff']);
                
                return myColour(this.heat);
            }
        },
    }
</script>

<style lang="css">
    .wrapper {
        display: flex;
        align-items: center;
        justify-content: center;
    }


    .range-input {
        display: flex;
        align-items: center;
        margin-bottom: 10px;
    }

    input,
    label {
        margin: 0 10px 0 5px;
    }
</style>
