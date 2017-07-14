<template>
  <div class="autocomplete-wrap">
    <input type="text"
           :id="id"
           :class="classname"
           :name="name"
           :placeholder="placeholder"
           v-model="inputmodel"
           @input="input(inputmodel)"
           @blur="hideAll"
           @focus="focus"/>
    <div v-if="showList" :class='"autocomplete autocomplete-"+ name ' :id="'autocomplete-'+ name ">
      <ul>
        <li v-for="data in json">
          <a href="javascript:void(0)"
             @click="selectList(data)">
            <b>{{ data[anchor] }}</b>
          </a>
        </li>
      </ul>
    </div>
  </div>
</template>

<script>

  //  import Vue from 'vue'
  //
  //  //转场效果
  //  Vue.transition('showAll',{});

  export default {
    props: {
      id: String,
      classname: String,
      name: String,
      placeholder: String,

      //父组件模型名称
      model: String,

      //JSON数据取值的Key
      anchor: {
        type: String,
        required: true
      },

      //请求的数据链接
      url: {
        type: String,
        required: true
      },

      //请求的参数KEY
      param: {
        type: String,
        default: 'q'
      },

      //拉取的数据个数的限制
      limit: {
        type: String,
        default: 5
      }
    },

    data () {
      return {
        showList: false,
        inputmodel: '',
        json: [],
        focusList: ''
      }
    },

    methods: {
      input (val) {
        this.showList = true;
        console.log("输入");
        //触发调用getData方法
        this.getData(val);
      },

      //隐藏补全列表
      hideAll (e) {

        //为了让blur方法延迟执行，以便能够成功执行click方法
        setTimeout(() => {
          this.showList = false;
        },250);

      },

      //
      focus (e) {
        this.focusList = 0;
      },

      //选中列表中的哪一项
      selectList (data) {
        console.log(data);
        console.log(JSON.stringify(data));

        //按照指定的JSON键值显示在模型上
        this.inputmodel = data.value;
        //传递给父组件中的对象
        this.showList = false;
      },

      //获取数据
      getData (val) {
        console.log(val);
        let self = this;

        if (this.url != null) {

          let ajax = new XMLHttpRequest();

          ajax.open('GET', `${this.url}?${this.param}=${val}`, true);
          ajax.send();

          ajax.addEventListener('progress', function (data) {
            if (data.lengthComputable) {
            }
          });

          ajax.addEventListener('loadend', function (data) {
            console.log(data);
            let json = JSON.parse(this.responseText);
            console.log(json);
            self.json = json;
          });

        }
      }

    },
//
  }
</script>

<style>
   .autocomplete, .autocomplete ul, .autocomplete ul li a {
    transition: all 0.3s ease-out;
    -moz-transition: all 0.3s ease-out;
    -webkit-transition: all 0.3s ease-out;
    -o-transition: all 0.3s ease-out;
  }

  .autocomplete ul {
    z-index: 999999;
    font-family: sans-serif;
    position: absolute;
    list-style: none;
    background: #f8f8f8;
    margin: 0;
    display: inline-block;
    /*min-width: 15%;*/
    width:100%;
    box-shadow: 0 0 5px rgba(0,0,0,.5);
    /*margin-top: 10px;*/
  }

  /*.autocomplete ul:before {*/
    /*content: "";*/
    /*display: block;*/
    /*position: absolute;*/
    /*height: 0;*/
    /*width: 0;*/
    /*border: 10px solid transparent;*/
    /*border-bottom: 10px solid #f8f8f8;*/
    /*top: -20px*/
  /*}*/

  .autocomplete ul li a {
    text-decoration: none;
    display: block;
    background: #f8f8f8;
    color: #2b2b2b;
    padding: 5px;
  }

  .autocomplete ul li a:hover, .autocomplete ul li.focus-list a {
    color: white;
    background: #2F9AF7;
  }

  /*.showAll-transition {*/
    /*opacity: 1;*/
    /*height: 50px;*/
    /*overflow: hidden;*/
  /*}*/

  /*.showAll-enter {*/
    /*opacity: 0.3;*/
    /*height: 0;*/
  /*}*/

  /*.showAll-leave {*/
    /*display: none;*/
  /*}*/

  /*.autocomplete-person {*/
    /*margin-left: 7px;*/
  /*}*/

</style>
