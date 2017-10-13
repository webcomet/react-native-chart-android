# react-native-chart-android
react-native-chart-android provide modules to add chart to android,all charts are come from mpandroidchart library,include bar chart ,line chart,combine chart etc.

 


### Installation

```
npm install react-native-chart-android --save
```

### Add it to your android project

* In `android/setting.gradle`

```gradle
include ':react-native-chart-android'
project(':react-native-chart-android').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-chart-android/android')
```

* In `android/app/build.gradle`

```gradle
...
dependencies {
  ...
  compile project(':react-native-chart-android')
}
```

* Register Module (in MainActivity.java)

```java
import cn.mandata.react_native_mpchart.MPChartPackage;  // <--- import

public class MainActivity extends ReactActivity {

    ......

    /**
     * A list of packages used by the app. If the app uses additional views
     * or modules besides the default ones, add more packages here.
     */
    @Override
    protected List<ReactPackage> getPackages() {
        return Arrays.<ReactPackage>asList(
                new MainReactPackage(),
                new ReactNativeIcons(Arrays.asList(
                        new IconFont("typicons", "typicons.ttf"),
                        new IconFont("fontawesome", "FontAwesome.otf")
                )),
                new MPChartPackage(),// <------ add this line to yout MainActivity class
                new ManDataLibPackage(),
                new BaiduVoiseLibPackage()
        );
    }
    ......
}
```

## Example
```javascript
/* @flow */
'use strict';

var React = require('react-native');
var TitleBar=require('./TitleBar');
var {
  BarChart,
  CombinedChart
}=require('../index.android');
var {
  StyleSheet,
  View,
  Text
} = React;

var Component = React.createClass({
  getBarData:function (argument) {
    var data={
      xValues:['1','2','3'],
      yValues:[
        {
          data:[4.0,5.0,6.0],
          label:'test1',
          config:{
            color:'blue'
          }
        },
        {
          data:[4.0,5.0,6.0],
          label:'test2',
          config:{
            color:'red'
          }
        },
        {
          data:[4.0,5.0,6.0],
          label:'test2',
          config:{
            color:'yellow'
          }
        }
      ]
    };  
    return data;
  },
  getRandomData:function (argument) {
    var data={};
    data['xValues']=[];
    data['yValues']=[
      {
        data:[],
        label:'test1',
        config:{
          color:'blue'
        }
      }
    ];
    for (var i = 0; i < 500; i++) {
      data.xValues.push(i+'');
      data.yValues[0].data.push(Math.random()*100);
    };
    return data;
  },
  render: function() {
    return (
      <View style={styles.container}>
        <TitleBar/>
        <View style={styles.chartContainer}>
          <BarChart style={{flex:1}} data={this.getBarData()}/>
         
          <BarChart 
            style={{flex:1}} 
            data={this.getRandomData()}
            visibleXRange={[0,30]}
            maxVisibleValueCount={50} 
                xAxis={{drawGridLines:false,gridLineWidth:1,position:"BOTTOM"}}
                yAxisRight={{enable:false}} 
                yAxis={{startAtZero:false,drawGridLines:false,position:"INSIDE_CHART"}}
                drawGridBackground={false}
                backgroundColor={"WHITE"} 
                description={"测试"}
                legend={{enable:true,position:'ABOVE_CHART_LEFT',direction:"LEFT_TO_RIGHT"}}
            />

           <LineChart 
             style={{flex:1}} 
             data={this.getRandomData()}
             visibleXRange={[0,30]}
             maxVisibleValueCount={50} 
             xAxis={{
              drawGridLines:false,
              gridLineWidth:1,
              position:"BOTTOM",
              labelRotationAngle: 12.0,
              spaceBetweenLabels: 10,
            }}
             yAxisRight={{enable:false}} 
             yAxis={{
              startAtZero:false,
              drawGridLines:true,
              position:"OUTSIDE_CHART",
              textColor: "#E94343"
              }}
             drawGridBackground={false}
             backgroundColor={"#FAFAFA"} 
             description={"Line Chart sample"}
             legend={{enable:true,position:'ABOVE_CHART_LEFT',direction:"LEFT_TO_RIGHT", legendForm: "CIRCLE"}}
             pinchZoom={true}
             dragDecelerationFrictionCoef={0.5}
             noDataText={"No data available"}
             onSelect={(e) => {
              console.log("onSelect xIndex", e.nativeEvent.xIndex, "yValue:", e.nativeEvent.yValue);
            }}
         />
        </View>
      </View>
    );
  }
});

var styles = StyleSheet.create({
  container:{
    flex:1
  },
  chartContainer:{
    flex:1
  },
  chart:{
    flex:1
  }
});


module.exports = Component;

 

There are some samples in sample folder,you can download them and try to run them.
## License
Web Comet