<template>
  <div class="emoji">
    <!--<ul class="emoji-controller">-->
      <!--<li-->
        <!--v-for="(pannel,index) in pannels"-->
        <!--@click="changeActive(index)"-->
        <!--:class="{'active': index === activeIndex}">{{ pannel }}</li>-->
    <!--</ul>-->
    <ul class="emoji-container">
      <li
        v-for="(emojiGroup, index) in emojis"
        style="padding: 0"
        :key="index"
        v-if="index === activeIndex">
        <a
          href="javascript:;"
          v-for="(emoji, index) in emojiGroup"
          :key="index" @click="selectItem(emoji)">
           <span
              class="emoji-item"
              :title="emoji"
              :class="'sprite-' + getPureName(emoji)"></span>
        </a>
      </li>
    </ul>
  </div>
</template>
<script>
import data from '@/components/common/data/emoji-data.js'
import  {chName} from '@/components/common/data/changeData.js'
export default {
  name: 'emoji',
  data () {
    return {
      emojiData: data,
      pannels: ['表情'],
      activeIndex: 0,
      transName:chName
    }
  },
  methods: {
    changeActive (index) {
      this.activeIndex = index
    },
    getPureName (name) {
      return name.replace(/:/g, '')
    },
    // 原先代码
    // selectItem (emoji) {
    //   this.$emit('select', emoji)
    // }

    // 修改后代码

    selectItem (emoji) {
      let emojiName
      for(let item of this.transName){
        for(let key in item){
          if(emoji == key){
            emojiName = item[key]
          }
        }

      }
      this.$emit('select', emojiName)
    }
  },
  computed: {
    emojis () {
      return this.pannels.map(item => {
        return Object.keys(this.emojiData[item])
      })
    }
  }
}
</script>

<style lang='scss' scoped>
@import '../common/scss/emoji-sprite.scss';

.emoji {
  width: 100%;
  height: 156px;
  bottom: 30px;
  background: #fff;
  z-index: 10;
  /*padding: 10px;*/
  /*margin-right: 10px;*/
  .emoji-controller {
    height: 36px;
    overflow: hidden;
    margin-bottom: 0;
    li {
      float: left;
      width: 76px;
      font-size: 12px;
      line-height: 36px;
      cursor: pointer;
      text-align: center;
      position: relative;
      &.active::after{
        content: '';
        width: 100%;
        height: 1px;
        background: #0689dd;
        left: 0;
        bottom: 4px;
        position: absolute;
      }
    }
  }
  .emoji-container {
    height: 140px;
    margin: 0;
    overflow-y: auto;
    overflow-x: hidden;
    position: relative;
    li {
      font-size: 0;
      padding: 5px;
      a {
        float: left;
        overflow: hidden;
        height: 35px;
        transition: all ease-out .2s;
        border-radius: 4px;
        &:hover {
          background-color: #d8d8d8;
          border-color: #d8d8d8;
        }
        span {
          width: 25px;
          height: 25px;
          display: inline-block;
          border: 1px solid transparent;
          cursor: pointer;
        }
      }
    }
  }
}
</style>
