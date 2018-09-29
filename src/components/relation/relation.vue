<template>
<div class="relation">
  <div class="main"></div>
</div>
</template>

<script>
import axios from 'axios'
import echarts from 'echarts'
export default {
  name: "relation",
  created() {
    this._getRelationData()
  },
  data() {
    return {
      color: this.$store.state.color,
      myChart: {},
      name: 'Relation'
    }
  },
  methods: {
    _init(options) {
      this.myChart = echarts.init(document.querySelector('.relation .main'))
      this.myChart.setOption(options)
      this.$root.charts.push(this.myChart)
      window.addEventListener('resize', function() {
        this.myChart.resize()
      }.bind(this))
    },
    _getRelationData: function () {
      axios.get('static/data/relations.json').then((res) => {
        let options;
        options = {
          title: {
            text: 'Edge Distribution'
          },
          animationDurationUpdate: 1500,
          animationEasingUpdate: 'quinticInOut',
          bmap: {
            center: [120.13066322374, 30.240018034923],
            zoom: 14,
            roam: true,
            mapStyle: {
              styleJson: [{
                'featureType': 'water',
                'elementType': 'all',
                'stylers': {
                  'color': '#d1d1d1'
                }
              }, {
                'featureType': 'land',
                'elementType': 'all',
                'stylers': {
                  'color': '#f3f3f3'
                }
              }, {
                'featureType': 'railway',
                'elementType': 'all',
                'stylers': {
                  'visibility': 'off'
                }
              }, {
                'featureType': 'highway',
                'elementType': 'all',
                'stylers': {
                  'color': '#fdfdfd'
                }
              }, {
                'featureType': 'highway',
                'elementType': 'labels',
                'stylers': {
                  'visibility': 'off'
                }
              }, {
                'featureType': 'arterial',
                'elementType': 'geometry',
                'stylers': {
                  'color': '#fefefe'
                }
              }, {
                'featureType': 'arterial',
                'elementType': 'geometry.fill',
                'stylers': {
                  'color': '#fefefe'
                }
              }, {
                'featureType': 'poi',
                'elementType': 'all',
                'stylers': {
                  'visibility': 'off'
                }
              }, {
                'featureType': 'green',
                'elementType': 'all',
                'stylers': {
                  'visibility': 'off'
                }
              }, {
                'featureType': 'subway',
                'elementType': 'all',
                'stylers': {
                  'visibility': 'off'
                }
              }, {
                'featureType': 'manmade',
                'elementType': 'all',
                'stylers': {
                  'color': '#d1d1d1'
                }
              }, {
                'featureType': 'local',
                'elementType': 'all',
                'stylers': {
                  'color': '#d1d1d1'
                }
              }, {
                'featureType': 'arterial',
                'elementType': 'labels',
                'stylers': {
                  'visibility': 'off'
                }
              }, {
                'featureType': 'boundary',
                'elementType': 'all',
                'stylers': {
                  'color': '#fefefe'
                }
              }, {
                'featureType': 'building',
                'elementType': 'all',
                'stylers': {
                  'color': '#d1d1d1'
                }
              }, {
                'featureType': 'label',
                'elementType': 'labels.text.fill',
                'stylers': {
                  'color': '#999999'
                }
              }]
            }
          },
          series: []
          // series: [
          //   {
          //     type: 'graph',
          //     layout: 'none',
          //     // progressiveThreshold: 700,
          //     data: res.data.nodes.map(function (node) {
          //       return {
          //         x: node.x,
          //         y: node.y,
          //         id: node.id,
          //         name: node.label,
          //         symbolSize: node.size,
          //         itemStyle: {
          //           normal: {
          //             color: node.color
          //           }
          //         }
          //       };
          //     }),
          //     edges: res.data.edges.map(function (edge) {
          //       return {
          //         source: edge.sourceID,
          //         target: edge.targetID
          //       };
          //     }),
          //     label: {
          //       emphasis: {
          //         position: 'right',
          //         show: true
          //       }
          //     },
          //     roam: true,
          //     focusNodeAdjacency: true,
          //     lineStyle: {
          //       normal: {
          //         width: 0.5,
          //         curveness: 0.3,
          //         opacity: 0.7
          //       }
          //     }
          //   }
          // ]
        };
        this._init(options)
      })
    }
  }
}
</script>

<style lang="stylus" scoped>
.relation
  height 800px
  .main
    height calc(100% - 120px)
    width 100%
    transition all 0.5s linear
</style>
