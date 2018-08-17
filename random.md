## Random stuff encountered throughout the day

### adding shadow for a view in swift

```swift
view.layer.masksToBounds = false;
view.layer.shadowOffset = CGSize(width: -3, height: 0)
view.layer.shadowRadius = 3;
view.layer.shadowOpacity = 0.25;
```

by drawing path
```swift
let shadowPath = UIBezierPath(rect: iconImageView.bounds)
iconImageView.layer.masksToBounds = false
iconImageView.layer.shadowColor = UIColor.black.cgColor
iconImageView.layer.shadowOffset = CGSize(width: -5, height: 5)
iconImageView.layer.shadowOpacity = 0.15
iconImageView.layer.shadowRadius = 7
iconImageView.layer.shadowPath = shadowPath.cgPath
```
