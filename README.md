# react-native-drop-refresh

A pull down to refresh control for react native.
This is a fork version from [Shuangzuan/RCTRefreshControl](https://github.com/Shuangzuan/RCTRefreshControl).

Better npm maintainess,issues are welcomed.

####Update 2.2.0 
Support react-native 0.40.0, change CMD to ES6 syntax.

####Update 2.1.0 
Support react-native 0.20.0, solve module name collsion issue.

## Screen Shot

![Screen Shot](screen-shot.gif)

## Installation

1. Run `npm install react-native-drop-refresh --save` in your project directory.
2. Run `react-native link` to link the lib up.
3. Add `import DropRefreshControl from 'react-native-drop-refresh';` to your code.

## Usage

```javascript
import React, { Component } from 'react';
import DropRefreshControl from 'react-native-drop-refresh';

import {
  AppRegistry,
  ListView,
  ScrollView,
  StyleSheet,
  Text,
  View
} from 'react-native';

var SCROLLVIEW = 'ScrollView';
var LISTVIEW = 'ListView';

class RCTRefreshControlDemo extends Component{
  constructor(){
    var ds = new ListView.DataSource({rowHasChanged: (r1, r2) => r1 !== r2});
    this.state = {
      dataSource: ds.cloneWithRows(['#484848', '#2F9C0A', '#05A5D1']),
    }
  }

  componentDidMount() {
    // ScrollView
    DropRefreshControl.configure({
      node: this.refs[SCROLLVIEW],
      tintColor: '#05A5D1',
      activityIndicatorViewColor: '#05A5D1'
    }, () => {
      setTimeout(() => {
        DropRefreshControl.endRefreshing(this.refs[SCROLLVIEW]);
      }, 2000);
    });

    // ListView
    DropRefreshControl.configure({
      node: this.refs[LISTVIEW]
    }, () => {
      setTimeout(() => {
        DropRefreshControl.endRefreshing(this.refs[LISTVIEW]);
      }, 2000);
    });
  }

  render() {
    return (
      <View style={styles.container}>
        <ScrollView ref={SCROLLVIEW} style={styles.scrollView}>
          <View style={{backgroundColor: '#05A5D1', height: 200}} />
          <View style={{backgroundColor: '#FDF3E7', height: 200}} />
          <View style={{backgroundColor: '#484848', height: 200}} />
        </ScrollView>

        <ListView
          ref={LISTVIEW}
          style={styles.listView}
          dataSource={this.state.dataSource}
          renderRow={(rowData) => {
            var color = rowData;
            return (
              <View style={{backgroundColor: color, height: 200}} />
            );
          }}
        />
      </View>
    );
  }
};

var styles = StyleSheet.create({
  container: {
    flex: 1,
    flexDirection: 'row'
  }
});

AppRegistry.registerComponent('DropRefreshControlDemo', () => DropRefreshControlDemo);
// use `export default DropRefreshControlDemo` instead to use this as an component;
```

---

## License

Available under the MIT license. See the LICENSE file for more informatiion.
