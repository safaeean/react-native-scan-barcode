# react-native-scan-barcode

A barcode scanner component for react native android. The library uses https://github.com/zxing/zxing to decode the barcodes. For iOS you can use https://github.com/lwansbrough/react-native-camera.

### React Native dependencies

- Version 0.1.4 for React Native <=0.18
- Version 1.x.x for React Native >=0.19
- Version 3.x.x for React Native >=0.25

### Installation

```bash
npm i --save react-native-scan-barcode
```

### Link it to your android project

You can link it simply by running `react-native link`.

#### Manual linking

* In `android/settings.gradle`

  ```gradle
  ...
  include ':react-native-scan-barcode', ':app'
  project(':react-native-scan-barcode').projectDir = new File(rootProject.projectDir, '../node_modules/react-native-scan-barcode/android')
  ```

* In `android/app/build.gradle`

  ```gradle
  ...
  dependencies {
      ...
      compile project(':react-native-scan-barcode')
  }
  ```

* register module (in MainApplication.java)

  Add the following **import** statement:
  ```Java
  import com.safaeean.barcodescanner.BarcodeScannerPackage;
  ```

  ...and then add `BarcodeScannerPackage` to exported package list *(MainApplication.java#getPackages)*:

  ```Java
  public class MainApplication extends Application implements ReactApplication {
      // (...)

      @Override
      protected List<ReactPackage> getPackages() {
        return Arrays.<ReactPackage>asList(
          new MainReactPackage(),
          new BarcodeScannerPackage()
        );
      }
  }
  ```

## Usage

```javascript
import React, {
  AppRegistry,
  Component,
} from 'react-native';
import BarcodeScanner from 'react-native-scan-barcode';

class ScanBarcodeApp extends Component {
  constructor(props) {
    super(props);

    this.state = {
      torchMode: 'off',
      cameraType: 'back',
    };
  }

  barcodeReceived(e) {
    console.log('Barcode: ' + e.data);
    console.log('Type: ' + e.type);
  }

  render() {
    return (
      <BarcodeScanner
        onBarCodeRead={this.barcodeReceived}
        style={{ flex: 1 }}
        torchMode={this.state.torchMode}
        cameraType={this.state.cameraType}
      />
    );
  }
}

AppRegistry.registerComponent('ScanBarcodeApp', () => ScanBarcodeApp);
```

## Example

Try the included [scan-barcode example](https://github.com/safaeean/react-native-scan-barcode/tree/master/Examples/scan-barcode) yourself:

```sh
git clone git@github.com:safaeean/react-native-scan-barcode.git
cd react-native-scan-barcode/Examples/scan-barcode
npm install
react-native run-android

```

To test the example you can scan the barcodes in the [Testcodes.pdf](https://github.com/safaeean/react-native-scan-barcode/tree/master/Examples/Testcodes.pdf) file.

## Properties

#### `onBarCodeRead`

Will call the specified method when a barcode is detected in the camera's view.
Event contains `data` (barcode value) and `type` (barcode type).
The following barcode types can be recognised:

```java
BarcodeFormat.UPC_A
BarcodeFormat.UPC_E
BarcodeFormat.EAN_13
BarcodeFormat.EAN_8
BarcodeFormat.RSS_14
BarcodeFormat.CODE_39
BarcodeFormat.CODE_93
BarcodeFormat.CODE_128
BarcodeFormat.ITF
BarcodeFormat.CODABAR
BarcodeFormat.QR_CODE
BarcodeFormat.DATA_MATRIX
BarcodeFormat.PDF_417
```

#### `torchMode`

Values:
`on`,
`off` (default)

Use the `torchMode` property to specify the camera torch mode.

#### `cameraType`

Values:
`back` (default),
`front`

Use the `cameraType` property to specify the camera to use. If you specify the front camera, but the device has no front camera the back camera is used.

### Viewfinder

The viewfinder is a child react component of the scan-barcode component. if you don't need the viewfinder (e.g. because you want your own child components to render) or you want your own viewfinder you can disable it with `showViewFinder={false}`.

The following properties can be used to style the viewfinder:

`viewFinderBackgroundColor`,
`viewFinderBorderColor`,
`viewFinderBorderWidth`,
`viewFinderBorderLength`,
`viewFinderShowLoadingIndicator`,

All color values are strings (e.g. '#eee' or 'rgba(0, 0, 0, 0.3)', default: 'white'). `viewFinderHeight` (default: 200), `viewFinderWidth` (default: 200), `viewFinderBorderWidth` (default: 2)and `viewFinderBorderLength` (default: 30) are numbers, `viewFinderShowLoadingIndicator` is either `true` or `false` (default) and shows a ActivityIndicator centered in the viewfinder.


http://yut.ir
http://mndco.ir
http://vistablog.ir
