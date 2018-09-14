---
title: 在react-native中使用mobx
date: 2018-09-03 15:54:09
tags:
  - mobx
categories:
  - mobx
---

1. ** 安装相应依赖：mobx 和 mobx-react **

    ```
    npm i mobx mobx-react --save
    ```

2. ** 安装一些 babel 插件，以支持 ES7 的 decorator 特性: **
   ```
   npm i babel-plugin-transform-decorators-legacy babel-preset-react-native-stage-0 --save-dev
   ```
3. ** 打开 .babelrc 没有就创建一个，配置 babel 插件: **
   ```
   touch .babelrc
   ```
   ** 写入 **
   ```
   {
   'presets': ['react-native'],
   'plugins': ['transform-decorators-legacy']
   }
   ```
   ** 补充:ES7 装饰器语法在编译器可能会报错；我这里用的是 vscode，分享解决办法： **
  1. 找到 首选项 > 设置 > 工作区设置;
  2. 加入以下代码：
   ```
   "javascript.implicitProjectConfig.experimentalDecorators": true
   ```

4. ** 加入 mobx **
   1. 根目录下新建 js 文件夹； js 下新建 store 文件夹；
   2. store 下新建 index.js 作用是合并每个 store 到一个 store 中去，最终通过Provider {...store}方式注入App
   3. 分别在 store 下新建几个 js，示例：
   ```
   class HomeStore {
   @observable text; // 注册变量，使其成为可检测的
   @observable num;
   constructor() {
   this.num = 0; // 初始化变量，可以定义默认值
   this.text = "Hello, this is homePage!!!";
   }
   @action // 方法推荐用箭头函数的形式
    plus = () => {
    this.num += 1;
    };

   @action
    minus = () => {
    this.num -= 1; 
    };
    }

   const homeStore = new HomeStore();

   export { homeStore };

    ```
    ```
    // user
    import { observable, action } from "mobx";

    class UserStore {
      @observable userInfo;
      @observable text;

      constructor() {
        this.userInfo = "123";
        this.text = "Hello, this is UserPage!!!";
      }

      @action
      getListData = () => {
        fetch(`http://yapi.demo.qunar.com/mock/5228/record/list`)
          .then(
            action("fetchRes", res => {
              return res.json();
            })
          )
          .then(
            action("fetchSuccess", data => {
              return (this.userInfo = data);
            })
          )
          .catch(
            action("fetchError", e => {
              console.log(e.message);
            })
          );
      };
    }

    const userStore = new UserStore();

    export { userStore };

    ```
5. ** 通过index文件合并 **
   ```
   import { homeStore } from "./home";
   import { userStore } from "./user";

   const store = { homeStore, userStore };

   export default store;

   ```
   
 6. ** 在组件中使用mobx **
  ```
    import { observer, inject } from "mobx-react"
    @inject(["homeStore"]) // 注入对应的store
    @observer // 监听当前组件
    class HomeScreen extends Component {
    constructor(props) {
      super(props);
      this.store = this.props.homeStore; //通过props来导入访问已注入的store
      this.state = {
      };
    }

    render() {
      const { text, num } = this.store;
      return (
        <Container>
          <Headers 
          title="首页" 
          type='index' 
          navigation={this.props.navigation}
          />
          <Text>{text}</Text>
          <Button primary onPress={() => this.store.plus()}>
            <Text>add</Text>
          </Button>
          <Text>{num}</Text>
          <Button primary onPress={() => this.store.minus()}>
            <Text>Minu</Text>
          </Button>
        </Container>
      );
    }
  }
  export default HomeScreen;

  ```
7. ** 目前组件中还拿不到当前组件的store，接下来注入store；**
   在初始化的项目结构中，项目运行的入口文件是index.js,注册了同级目录下的App.js;

   ```
    // index.js

    import { AppRegistry } from 'react-native';
    import App from './App';

    AppRegistry.registerComponent('demo', () => App);

   ```
   由于需要在App.js上套入store 所以改写结构，
   1. 新建setup.js文件
      ```
import React from "react";
import { Provider } from "mobx-react";
import App from "./App";
import store from "./store";

export default function setup() {
  class Root extends React.Component {
    render() {
      return (
        <Provider {...store}>
          <App />
        </Provider>
      );
    }
  }
  return Root;
}
      ```
  2. 修改index启动页代码
  ```
import { AppRegistry } from 'react-native';
import setup from "./js/setup";

AppRegistry.registerComponent('******', () => setup());
  ```