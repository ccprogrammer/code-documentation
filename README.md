# code-documentation

<br />

### # Adding Item + Creating The Model that contain list with another model
1. The parent/first model that contain a list and it will be filled with another model
```
 class ItemModel {
  int id;
  String itemName;
  List itemList;
  SetModel({
    required this.id,
    required this.itemName,
    required this.itemList,
  });
```

2. This model will be add to the first model (ItemModel) List/itemList 
```
class ItemListModel {
  int id;
  String itemListModelName;
  ComboModel({
    required this.id,
    required this.itemListModelName,
  });
}
```

3. In the add function in ItemModel.itemList defined what the list is from, we define it from ItemListModel so when we add item in ItemListModel it will automatically listed in the ItemModel.itemList.

```
  void addItem(id, itemName) {
    setList.add(
      ItemModel(
        id: id,
        itemName: itemName,
        itemList: <ItemListModel>[],
      ),
    );
  }
```

4. All this will result something like for example:
```
 1. i add 2 parent item/first model
 2. 2 item appear
 3. i click parent item 1 and add list/ItemListModel in it
 4. when i click in parent item 2 the list that i add before doesn't appear but it will only appear in parent item 1
```

### # Remove Item
1. This will remove item that are picked from looping/item builder index, i is the index from looping/item builder
```
 item.removeAt(id);
 
 example: 
 for (var i = 0; i < widget.item.comboList.length; i++)
                      ComboTile(
                        item: list[i],
                        onDelete: () {
                          item.removeAt(i);
                        },
                      ),
```

2. This will remove item if the item id is the same as the item id that are select/item that pressed to be remove
```
item.removeWhere(
      (element) => element.id == id,
    );
```
