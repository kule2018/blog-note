[toc]

# react-native 入门基础介绍

> 一个简单的demo，用于介绍react-native相关基础信息，主要是针对有兴趣的同学参考；以下内容及代码在2018-08测试有效。

> 完整项目代码：[https://github.com/NameHewei/react-native](https://github.com/NameHewei/react-native)


# 安装
1. npm install -g create-react-native-app
2. create-react-native-app you-app-name
3. cd you-app-name
4. npm start
5. download Expo app：https://expo.io/（可能要注册）在手机上安装
6. 扫描 npm start 后显示的二维码

**为了项目顺利，请备好梯子！**

这里是通过在手机上安装Expo，然后用Expo扫描启动项目后生成的二维码来预览你的react-native项目，前提是PC的IP要与手机的IP在同一个网段内。Expo打包你的项目后，每次PC端Ctrl+S都会自动更新Expo的内容。本文不介绍安装模拟器的开发方式，需要的请自行Google。

# 项目
## 主要目录结构
```
|—— app.js
|—— view
  |—— Home.js
    |—— cookbook
        |—— Cookbook.js
        |—— Detail.js
        |—— List.js
    |—— novel
        |—— Novel.js
```

以下所有涉及组件属性请参考文章最后官网链接进行查看，本文只对关键属性作说明。

路由组件使用：react-native

UI组件使用：native-base

## 入口
```js
export default createDrawerNavigator({
    home: {
        screen: Home
    },
    novel: {
        screen: Novel
    },
    cookbook: {
        screen: Cookbook
    },
}, {
    drawerBackgroundColor: '#ffffff',
    contentOptions: {
        activeTintColor: '#e91e63',
    }
});
```
首页使用侧滑（createDrawerNavigator）路由组件，默认显示路由为对象的第一个属性值。

### Home模块
```js
export default class Home extends Component {
    static navigationOptions = {
        drawerLabel: 'Home',
        drawerIcon: ({ tintColor }) => (
            <Image
                source={require('./../public/img/menu.png')}
                style={[styles.icon, { tintColor: tintColor }]}
            />
        ),
    };

    render() {
        return (    
            <View
                style={{ flex: 1, marginTop: 20 }}
            >
                <View
                    style={{ flex: 1, alignItems:'center', justifyContent: 'center' }}
                >
                    <TouchableHighlight 
                        underlayColor={ '#fff' }
                        activeOpacity={ 1 }
                        onPress={ () => this.props.navigation.openDrawer() }>
                        <Image
                            style={{ height: 220, width: 220, borderRadius: 110 }}
                            source={require('./../public/img/avatar.jpg')}
                        />
                     </TouchableHighlight>
                </View>
            </View>
        );
    }
}
```
该页面主要是首屏显示内容，根据页面代码注意以下三点:
1. 图片链接要用TouchableHighlight
2. 使用navigation.openDrawer()方法打开侧滑
3. 图片地址要用require(url)方法引入

### Coobook模块
```js
const navigationConfig = {
    header: null
}

export default App = createStackNavigator({
    List: {
        screen: List,
        path: 'list/:id',
        navigationOptions: (navigation) => (navigationConfig)
    },
    Detail: { 
        screen: Detail,
        navigationOptions: (navigation) => ({
            title: '详情'
        })
    },
})
``` 

cook模块功能是提供一个列表页，点击列表项进入详情页，注意以下三点：
1. 用createStackNavigator路由组件实现。
2. List 页面不需要顶部的header所以设置为null(具体参见文档)
3. 因为详情页需要id这里可以用list/:id传参

### List模块
```js
export default class ListComponent extends Component {
    render() {
        return (    
            <View
                style={{ flex: 1, paddingTop: 20 }}
            >
                <Container>
                    <Content>
                        <List>
                            <ListItem avatar onPress={() => {
                                this.props.navigation.navigate('Detail', {
                                    id: 0
                                })
                            }}>
                                <Left>
                                    <Thumbnail source={{ uri: 'http://xx.jpg' }} />
                                </Left>
                                <Body>
                                    <Text>回锅肉</Text>
                                    <Text note>一道好吃到板的菜</Text>
                                </Body>
                                <Right>
                                    <Text note>2018-08-21</Text>
                                </Right>
                            </ListItem>
                    </List>
                    </Content>
                </Container>

            </View>

        );
    }
}
```
该组件用到了native-base UI组件

注意以下四点：
1. 注意组件只能用提供的，style的属性也是只能用提供的。
2. 顶部菜单栏高为20 ，所有宽高都不需要加单位，会自动转化为设备单位
3. 文字必须要用Text包裹
4. 路由跳转由navigation.navigate('name', params)实现

### novel模块
```js
export default createBottomTabNavigator({
    Home: {
        screen: HomeScreen,
        navigationOptions: () => ({
            tabBarVisible : true,
            title: '蚂蚁国度',
            headerBackTitle: null
        }), 
    },
    Settings: {
        screen: SettingsScreen,
        navigationOptions: () => ({
            tabBarVisible : true,
            title: '最强神级兵王',
            headerBackTitle: null
            }),
    },
    }, {
        headerMode: 'screen',
    });
```
该模块采用在底部点击菜单按钮的形式来查看不同小说，所以采用新的路由方式：
1. 使用createBottomTabNavigator切换screen
2. 页面内容多需要滑动，需用ScrollView组件包裹

# 相关参考
- RN官网：https://facebook.github.io/react-native/
- React Navigation官网: https://reactnavigation.org/
- nativeBase组件:https://nativebase.io/


> 若有疑问或错误，请留言，谢谢！[Github blog issues](https://github.com/NameHewei/blog/issues)


