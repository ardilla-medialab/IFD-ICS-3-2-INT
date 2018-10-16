<template>
    <div class="data-visualization">
        <!--
        <div class="country-selection">
            <div class="field">
                <label class="label">Selecciona un país</label>
                <div class="control">
                    <div class="select country-selection">
                        <select v-model="selectedCountry">
                            <option disabled value="">Selecciona un país</option>
                            <option>Select dropdown</option>
                            <option>With options</option>
                        </select>
                    </div>
                </div>
            </div>
        </div>
        -->
        <div class="line-graph">

        </div>
    </div>
</template>

<script>
    /* eslint-disable no-console,no-unused-vars */

    import * as d3 from "d3";

    import countriesJson from '../assets/data/cc'

    export default {
        name: 'DataVisualization',
        props: {},
        data: function () {
            return {
                selectedCountry: '',
                vis: {
                    width: 0,
                    svg: null
                }
            }
        },
        mounted: function () {
            console.log("DataVisualization mounted");
            this.getDimensions();
            this.drawVis();
        },
        methods: {
            getDimensions: function () {
                let dimensions = d3.select(".data-visualization").node().getBoundingClientRect();
                this.vis.width = dimensions.width;
                this.vis.height = dimensions.width * 0.5;
            },
            drawVis: function () {
                this.svg = d3.select(".line-graph")
                    .append("svg")
                    .attr("width", this.vis.width)
                    .attr("height", this.vis.height);

                const yScale = d3.scaleLinear()
                    .domain([-2.5, 2.5])
                    .range([this.vis.height - 50, 0]);

                const yAxis = d3.axisLeft().scale(yScale);
                yAxis.tickFormat(d3.format(',.1f'));
                yAxis.tickSizeInner(5);
                yAxis.tickSizeOuter(5);
                yAxis.tickPadding(5);
                yAxis.tickValues([-2.5, 0, 2.5]);

                const yAxisRight = d3.axisRight().scale(yScale);
                yAxisRight.tickFormat(d3.format(',.1f'));
                yAxisRight.tickSizeInner(5);
                yAxisRight.tickSizeOuter(5);
                yAxisRight.tickPadding(5);
                yAxisRight.tickValues([-2.5, 0, 2.5]);

                let yAxisLeftX = (this.vis.width / 2 - this.vis.width / 4);
                let yAxisRightX = (this.vis.width / 2 + this.vis.width / 4);

                this.svg.append("g")
                    .attr("class", "axis")
                    .attr("transform", "translate(" + yAxisLeftX + ",10)")
                    .call(yAxis);

                this.svg.append("text")
                    .attr("x", yAxisLeftX)
                    .attr("y", yScale(-2.5) + 35)
                    .style("text-anchor", "middle")
                    .text("1996");

                this.svg.append("g")
                    .attr("class", "axis")
                    .attr("transform", "translate(" + yAxisRightX + ",10)")
                    .call(yAxisRight);

                this.svg.append("text")
                    .attr("x", yAxisRightX)
                    .attr("y", yScale(-2.5) + 35)
                    .style("text-anchor", "middle")
                    .text("2017");

                this.svg.append("g")
                    .selectAll("line")
                    .data(countriesJson.data)
                    .enter()
                    .append("line")
                    .attr("class", "line")
                    .attr("x1", yAxisLeftX)
                    .attr("y1", function (d) {
                        return yScale(d.a1996);
                    })
                    .attr("x2", yAxisRightX)
                    .attr("y2", function (d) {
                        return yScale(d.a2017);
                    })

            }
        }
    }
</script>

<style lang="scss">
    .data-visualization {
        padding: 5px;
        min-height: 100px;
        background-color: #fff;
    }

    .axis {
        stroke-width: 0.5px;
        stroke: black;
    }

    .line {
        stroke-width: 2px;
        stroke-opacity: 0.7;
        stroke: grey;
        transition: stroke-width 0.3s ease-in;
        &:hover {
            cursor: pointer;
            stroke-width: 3px;
            transition: stroke-width 0.3s ease-out;
        }
    }

</style>
