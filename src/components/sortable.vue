<template>
  <div class="page-sortable">
    <div class="sortable">
      <div class="headline">
        <div class="small">
          <h3>{{data.editRegion.name}}</h3>
        </div>
      </div>
      <div class="draggable-module">
        <draggable
                class="draggable-left"
                :options="optionsLeft"
                :list="data.editRegion.content"
                @add="onAdd">
          <transition-group tag="ul" class="tagTableLeft">
            <li v-for="item in data.editRegion.content" :key="item.id" >
              {{item.title}}
            </li>
          </transition-group>
        </draggable>
        <div class="placeholder" v-if="data.editRegion.content.length == 0">
          <h1>添加元素</h1>
        </div>
      </div>
    </div>
    <div class="tag-table">
      <h3>{{data.selectRegion.name}}</h3>
      <draggable
              class="draggable-right"
              :list="data.selectRegion.content"
              handle=".handle"
              :options="optionsRight">
        <transition-group tag="ul">
          <li v-for="(item) in data.selectRegion.content" :key="item.id" class="handle">
            <p>{{item.title}}</p>
          </li>
        </transition-group>
      </draggable>
    </div>
  </div>
</template>

<script>
    import {lists} from './data'
    import draggable from 'vuedraggable';
    export default {
        data(){
            return{
                data: lists
            }
        },
        components:{
            draggable
        },
        computed:{
            optionsLeft(){
                return {
                    animation: 0,
                    group: "items",
                }
            },
            optionsRight(){
                return {
                    animation: 150,
                    group: {
                        name: "items",
                        pull: 'clone'
                    }
                }
            }
        },
        methods:{
            onAdd(e){
                var oldIndex=e.oldIndex
                this.data.selectRegion.content.splice(oldIndex,1)
            }
        }
    }
</script>

<style>
  .tag-table{
    position: absolute;
    right: 0;
    top: 0px;
    margin-right: 0;
    width: 249px;
    height: 100%;
    box-shadow: 0 1px 12px rgba(0, 0, 0, 0.08);
    background: #fff;
    border: 1px solid #ddd;
    overflow: auto;
    box-sizing: border-box;
  }
  h3{
    padding: 12px 0;
    font-size: 16px;
    text-align: center;
    background-color:#6593aa;
    color: #fff;
  }

  p{
    color: #333;
    padding: 10px 14px;
    cursor: move;
    border-bottom: 1px dashed #ddd;
  }
  p:hover{
    box-shadow: 0 1px 12px rgba(0,0,0,.3);
  }
  .page-sortable{
    width: 100%;
    position: relative;
    padding-right: 259px;
    box-sizing: border-box;
  }
  .draggable-module{
    position: relative;
  }

  .draggable-left{
    padding: 20px;
  }
    .tagTableLeft{
      width: 100%;
      min-height: 200px;
      margin-top: 20px;
    }
    .tagTableLeft li{
      cursor: move;
      margin-bottom: 6px;
      width: 100%;
      min-height: 70px;
      background: #f6f6f6;
      border: 1px solid #ddd;
      border-radius: 4px;
      padding: 8px;
      box-sizing: border-box;
    }

    .placeholder{
      position: absolute;
      top: 20px;
      left: 20px;
      z-index: 0;
      text-align: center;
      width: calc(100% - 40px);
      padding: 120px 0;
      border: dashed 1px #DCDCDC;
      text-align: center;
    }
  .placehoder p{
    padding-top: 20px;
  }
  .placeholder h1{
    font-size: 20px;
  }
</style>

