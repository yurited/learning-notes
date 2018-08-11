Table and Collection Views

### The UITableView/CollectionViewDataSource Protocol
The "data retrieving" protocol has many methods.

**UITableView**
`func numberOfSections(in tableView: UITableView) -> Int`
`func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int`
`func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell`

**UICollectionView**
`func numberOfSections(in collectionView: UICollectionView) -> Int`
`func collectionView (_ collectionView: UICollectionView, numberOfRowsInSection section: Int) -> Int`
`func collectionView(_ collectionView: UITableView, cellForRowAt indexPath: IndexPath) -> UICollectionViewCell`
IndexPath specifies with row(in tableView) or item(in collectionView).
In both, you get the section the row or item is in from `indexPath.section`

In tableView, you get which row from `indexPath.row`; in collectionView you get which item from `indexPath.item`.

CollectionView might seem like rows and columns, but it's not, it's just items "flowing" like text.


### Putting data into the UI
```
func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
    let prototype = decision ? "FoodCell" : "CustomFoodCell"
    let cell = tableView.dequeueResuableCell(withIndentifier: prototype, for: indexPath)
    if let myCell = cell as? MyCell {
        // set data
    }
    ...
}
```


### Table View Segues

```
func prepare(for segue: UIStoryboardSegue, sender:Any?) {
    if let identifier = segue.identifier {
        switch identifier {
            case "OtherSegue":
            case "MySegue":
                if let cell = sender as? MyTableViewCell,
                   let indexPath = tableview.indexPath(for: cell),
                   seguedToMVC = segue.destination as? MyVC {
                       seguedToMVC.publicAPI = data[indexPath.section][indexPath.row]
                   }
            default: break
        }
    }
}
```
**Seguing from Collection View cells**
probably best done from this `UICollectionViewDelegate` method
`func collectionView(collectionView: UICollectionView, didSelectItemAtIndexPath indexPath: IndexPath)`

`Use performSegue(withIndentifier:)` from here

(can also send `IndexPath` thru `Any?`)


### Reload

`func reloadData`
reload all visible cells

`func reloadRows(at indexPaths [indexPath], with animation: UITableViewRowAnimation)`


## Height

**TableView**

Row height can be fixed (UITableView's `var rowHeight: CGFloat`)
Or it can be determined using autolayout (`rowHeight = UITableViewAutomaticDimension`)

I fyou do automatic, help the table view out by setting `estimatedRowHeight` to something

UITableView's delegate can also control row heights:

`func tableView(UITableView, {estimated}heightForRowAt indexPath: IndexPath) -> CFFloat`
Beware: the non-estimated version of this could get called **a lot** if you  you have a big table.


**CollectionView**

Cell size can be fixed in the storyboard

You can also drive it from autolayout similar to table view

or you can return from delegate method
```
func collectionView(_ collectionView: UICollectionView,
                    layout collectionViewLayout: UICollectionViewLayout,
                    sizeForItemAt indexPath: indexPath) -> CGSize
```


### Headers
Collection View header are also reusable
