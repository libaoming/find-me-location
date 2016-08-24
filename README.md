# find-me-location

### Add CoreLocation Kit  reference: project > build phase > link binaries with lib > coreLocation framework


*** 

####  Add key in info.plist

> NSLocationWhenInUseUsageDescription &nbsp; &nbsp; &nbsp; Type String <br>
  NSLocationAlwaysUsageDescription     &nbsp; &nbsp; &nbsp; Type String
  
  
***


### import coreLocation kit in .swift, add CLLocationManagerDelegate to UIViewController class

```swift
class ViewController: UIViewController, CLLocationManagerDelegate, MKMapViewDelegate
```

### import mapkit, add MKMapviewDelegate in UIViewController 

```swift
class ViewController: UIViewController, CLLocationManagerDelegate, MKMapViewDelegate
```

### locationManger setup

```swift
        locationManager.delegate = self
        locationManager.desiredAccuracy = kCLLocationAccuracyBest
        locationManager.requestWhenInUseAuthorization()
        locationManager.startUpdatingLocation()
```

### locationManger updateLocation func 

```swift
    func locationManager(_ manager: CLLocationManager, didUpdateLocations locations: [CLLocation]) {
      
        let userLocation = locations[0]
        
        let latitude = userLocation.coordinate.latitude
        let longtitude = userLocation.coordinate.longitude
        
        let longDelta: CLLocationDegrees = 0.05
        let latiDelta: CLLocationDegrees = 0.05
        
        let center = CLLocationCoordinate2D(latitude: latitude, longitude: longtitude)
        let span = MKCoordinateSpan(latitudeDelta: latiDelta, longitudeDelta:longDelta)
        
        
        let region = MKCoordinateRegion(center: center, span: span)
        
        map.setRegion(region, animated: true)
        
        let annotation: MKPointAnnotation = MKPointAnnotation()
        
        annotation.coordinate.latitude = latitude
        annotation.coordinate.longitude = longtitude
        
        map.addAnnotation(annotation)
        
        
        
    }
}
```

