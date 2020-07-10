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
            "id": "silkysky",
            "countryCode": null,
            "pid": null,
            "level": 0,
            "center": 1,
            "countProduct": 0,
            "countryImg": null
          },
          {
            "id": "bpsimon77",
            "countryCode": "82",
            "pid": "silkysky",
            "level": 0,
            "center": 1,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "cho6667",
            "countryCode": "82",
            "pid": "bpsimon77",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "yoon3001",
            "countryCode": "82",
            "pid": "cho6667",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "chyoon9732",
            "countryCode": "82",
            "pid": "bpsimon77",
            "level": 0,
            "center": 1,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "do1246",
            "countryCode": "82",
            "pid": "chyoon9732",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "lyj9632",
            "countryCode": "82",
            "pid": "do1246",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "psm3993",
            "countryCode": "82",
            "pid": "do1246",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "rsh1890",
            "countryCode": "82",
            "pid": "do1246",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "sms3107",
            "countryCode": "82",
            "pid": "do1246",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "cyj6159",
            "countryCode": "82",
            "pid": "do1246",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "aa1246",
            "countryCode": "82",
            "pid": "do1246",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "yjh80180",
            "countryCode": "82",
            "pid": "do1246",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "jinyu2204",
            "countryCode": "82",
            "pid": "do1246",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "byy18880",
            "countryCode": "82",
            "pid": "do1246",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "inza6904",
            "countryCode": "82",
            "pid": "chyoon9732",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "jungsuna90",
            "countryCode": "82",
            "pid": "chyoon9732",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "kim3259",
            "countryCode": "82",
            "pid": "chyoon9732",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "q6957",
            "countryCode": "82",
            "pid": "kim3259",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "soon404",
            "countryCode": "82",
            "pid": "kim3259",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "kim503826",
            "countryCode": "82",
            "pid": "chyoon9732",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "ok4800",
            "countryCode": "82",
            "pid": "chyoon9732",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "pahan72",
            "countryCode": "82",
            "pid": "chyoon9732",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "qwe754100",
            "countryCode": "82",
            "pid": "chyoon9732",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "sook433600",
            "countryCode": "82",
            "pid": "qwe754100",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "sww3658",
            "countryCode": "82",
            "pid": "qwe754100",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "xotjd1704",
            "countryCode": "82",
            "pid": "qwe754100",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "jayar202",
            "countryCode": "82",
            "pid": "qwe754100",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "kus754100",
            "countryCode": "82",
            "pid": "qwe754100",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "sy3bae",
            "countryCode": "82",
            "pid": "chyoon9732",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "duc1455",
            "countryCode": "82",
            "pid": "sy3bae",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "angelina12",
            "countryCode": "82",
            "pid": "sy3bae",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "sy3bae1 ",
            "countryCode": "82",
            "pid": "sy3bae",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "sgg015a",
            "countryCode": "82",
            "pid": "sy3bae",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "fasttur",
            "countryCode": "82",
            "pid": "sy3bae",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "chs1127",
            "countryCode": "82",
            "pid": "sy3bae",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "sy7746",
            "countryCode": "82",
            "pid": "chyoon9732",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "ssd3000",
            "countryCode": "82",
            "pid": "chyoon9732",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "choi68",
            "countryCode": "82",
            "pid": "chyoon9732",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "song73",
            "countryCode": "82",
            "pid": "choi68",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "wnsska72",
            "countryCode": "82",
            "pid": "chyoon9732",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "wnsska1972",
            "countryCode": "82",
            "pid": "chyoon9732",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "go9139",
            "countryCode": "82",
            "pid": "chyoon9732",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "chyoon9731",
            "countryCode": "82",
            "pid": "chyoon9732",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "d5335",
            "countryCode": "82",
            "pid": "bpsimon77",
            "level": 0,
            "center": 1,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "sky99",
            "countryCode": "82",
            "pid": "d5335",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "raffineko",
            "countryCode": "82",
            "pid": "sky99",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "mmhee",
            "countryCode": "82",
            "pid": "sky99",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "red77",
            "countryCode": "82",
            "pid": "sky99",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "sung556",
            "countryCode": "82",
            "pid": "d5335",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "kjs1929 ",
            "countryCode": "82",
            "pid": "sung556",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "jkh7748",
            "countryCode": "82",
            "pid": "sung556",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "sms9921",
            "countryCode": "82",
            "pid": "sung556",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "goty59",
            "countryCode": "82",
            "pid": "sung556",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "ksg567",
            "countryCode": "82",
            "pid": "bpsimon77",
            "level": 0,
            "center": 1,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "ace8165",
            "countryCode": "82",
            "pid": "ksg567",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "jg6012",
            "countryCode": "82",
            "pid": "ksg567",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "seongho6163",
            "countryCode": "82",
            "pid": "ksg567",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "snklove2030",
            "countryCode": "82",
            "pid": "ksg567",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "th6401",
            "countryCode": "82",
            "pid": "ksg567",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "marchout1",
            "countryCode": "82",
            "pid": "bpsimon77",
            "level": 0,
            "center": 1,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "arrow1",
            "countryCode": "82",
            "pid": "marchout1",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "arrow2",
            "countryCode": "82",
            "pid": "arrow1",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "arrow3",
            "countryCode": "82",
            "pid": "arrow1",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "arrow4",
            "countryCode": "82",
            "pid": "arrow1",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "arrow5 ",
            "countryCode": "82",
            "pid": "arrow1",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "arrow6",
            "countryCode": "82",
            "pid": "arrow1",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "arrow7",
            "countryCode": "82",
            "pid": "arrow1",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "arrow8",
            "countryCode": "82",
            "pid": "arrow1",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "arrow9",
            "countryCode": "82",
            "pid": "arrow1",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "arrow10",
            "countryCode": "82",
            "pid": "arrow1",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "arrow11",
            "countryCode": "82",
            "pid": "arrow1",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "csc",
            "countryCode": "82",
            "pid": "marchout1",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "csm",
            "countryCode": "82",
            "pid": "marchout1",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "hysepksc",
            "countryCode": "82",
            "pid": "marchout1",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "nort",
            "countryCode": "82",
            "pid": "marchout1",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "nort1",
            "countryCode": "82",
            "pid": "marchout1",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "park2351",
            "countryCode": "82",
            "pid": "marchout1",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "park2352",
            "countryCode": "82",
            "pid": "marchout1",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "sym73",
            "countryCode": "82",
            "pid": "marchout1",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "terry",
            "countryCode": "82",
            "pid": "marchout1",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "terry1",
            "countryCode": "82",
            "pid": "marchout1",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "marchout2",
            "countryCode": "82",
            "pid": "bpsimon77",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "okman",
            "countryCode": "82",
            "pid": "bpsimon77",
            "level": 0,
            "center": 1,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "osim",
            "countryCode": "82",
            "pid": "okman",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "jy0620",
            "countryCode": "82",
            "pid": "osim",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "hskim",
            "countryCode": "82",
            "pid": "osim",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "misso",
            "countryCode": "82",
            "pid": "osim",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          },
          {
            "id": "soo0447",
            "countryCode": "82",
            "pid": "okman",
            "level": 0,
            "center": 0,
            "countProduct": null,
            "countryImg": "https://manage.silkyskyglobal.com:2087/silkysky/resources/images/countryCode/82.png"
          }
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