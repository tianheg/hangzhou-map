<script>
import AMapLoader from '@amap/amap-jsapi-loader'
import { shallowRef } from '@vue/reactivity'

const MAP_KEY = import.meta.env.VITE_MAP_KEY

export default {
  name: 'HangzhouMap',
  setup() {
    const map = shallowRef(null)
    return {
      map,
    }
  },
  create() {},
  mounted() {
    //DOM初始化完成进行地图初始化
    this.ininMap()
  },
  methods: {
    ininMap() {
      AMapLoader.load({
        key: `${MAP_KEY}`,
        version: '2.0',
        plugins: ['AMap.ToolBar', 'AMap.Driving'],
        AMapUI: {
          version: '1.1',
          plugins: [],
        },
        Loca: {
          version: '2.0.0',
        },
      })
        .then((AMap) => {
          this.map = new AMap.Map('container', {
            zoom: 12,
            zooms: [3, 20],
            center: [120.183768, 30.244367],
          })
        })
        .catch((e) => {
          console.log(e)
        })
    },
    addMarker() {},
  },
}
</script>
<template>
  <div class="home_div">
    <div class="map-title">
      <h3>高德地图 + Vue3</h3>
    </div>
    <div id="container" />
  </div>
</template>

<style scope>
.home_div {
  height: 100%;
  width: 100%;
  padding: 0px;
  margin: 0px;
  position: relative;
}
#container {
  height: 100%;
  width: 100%;
  padding: 0px;
  margin: 0px;
}
.map-title {
  position: absolute;
  z-index: 1;
  width: 100%;
  height: 50px;
  background-color: rgba(27, 25, 27, 0.884);
}
h3 {
  position: absolute;
  left: 10px;
  z-index: 2;
  color: white;
}
</style>
