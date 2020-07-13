<template>
  <div class="tree">

    <svg ref="svg" :width="viewer.w" :height="viewer.w" @click="setZoom" style="touch-action: none; -webkit-tap-highlight-color: rgba(0, 0, 0, 0);">
      <g :transform="`translate(${zoom.x},${zoom.y})scale(${zoom.k})`">
        <path class="link" v-for="line in lines" :d="getDiagonal(line)" stroke="#333" stroke-width="1" fill="none">
        </path>
        <g class="node" v-for="node in nodes" :transform="`translate(${node.x},${node.y})`">
          <rect fill="#313642" stroke="#313642" stroke-width="1" width="150" height="25">
          </rect>
          <text fill="#fff" y="18" x="40" style="font-size:11px;" text-anchor="start">{{node.data.id}} (김떙땡)</text>
          <image :href="node.data.countryImg" height="30" width="30" x="3" y="-2"/>
          <rect fill="#fff" stroke="#313642" stroke-width="1" width="150" height="25" y="25">
          </rect>
          <text fill="#333" y="42" x="38" style="font-size:11px;" text-anchor="start">코드구매갯수 : 3</text>

        </g>
        
      </g>
      
    </svg>
    
  </div>
</template>

<script>
  import * as d3 from 'd3'
  export default {
    name: 'tree',
    data () {
      return {
        viewer: {
          w: 600,
          h: 600
        },
        a:[],
        nodes: [],
        lines: [],
        zoom: {
          x: 40,
          y: 0,
          k: 0.2
        },
        data:[
          {
            "id": "cryu",
            "countryCode": null,
            "pid": null,
          },
          {
            "id": "mai",
            "countryCode": "82",
            "pid": "cryu",
          },
          {
            "id": "cherin",
            "countryCode": "82",
            "pid": "mai",
          },
          {
            "id": "takasaki",
            "countryCode": "82",
            "pid": "cryu",
          },
          {
            "id": "otoko",
            "countryCode": "82",
            "pid": "mai",
          },
          {
            "id": "sam",
            "countryCode": "82",
            "pid": "cherin",
          },
        ]
      }
    },
    created () {
      // this.setData()
      this.viewer.w = window.innerWidth;
    },
    async mounted () {
      await this.d3Set();
      await this.setZoom()

    },
    methods: {
      d3Set() {
        const stratify = d3.stratify().id(d=>d.id).parentId(d => d.pid)
        // const tree = d3.tree().size([2000, 2000]);
        const tree = d3.tree().nodeSize([230,300]);

        const rootNode = stratify(this.data);
        const treeData = tree(rootNode);

        this.nodes = rootNode.descendants();

        this.lines = this.nodes.slice(1);

        
      },
      onZoom () {
        this.zoom.x = d3.event.transform.x
        this.zoom.y = d3.event.transform.y
        this.zoom.k = d3.event.transform.k
      },
      setZoom () {
        const zoom = d3.zoom().scaleExtent([0.2, 5]).on('zoom', this.onZoom)
        const selection = d3.select(this.$refs.svg)
        selection
          .call(zoom)
          .call(zoom.transform, this.initZoom())
      },
      initZoom () {
        this.zoom.x = 40
        this.zoom.y = 0
        this.zoom.k = 0.2
        return d3.zoomIdentity
          .translate(this.zoom.x, this.zoom.y)
          .scale(this.zoom.k)
      },
       getDiagonal (d) {
        // return `M${d.x+75},${d.y} C${d.x+75},${d.y} ${d.parent.x+75},${d.parent.y+50} ${d.parent.x+75}, ${d.parent.y + 50}`
        return `M${d.x+75},${d.y} C${d.x+75},${d.parent.y+50} ${d.parent.x+75},${d.y} ${d.parent.x+75}, ${d.parent.y+50} `
      },
      
    }
  }
</script>

<style>
</style>