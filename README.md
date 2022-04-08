# Flutter Code Documentation 

<br />

## Misc

### # Datetime
1. DateTime.now() will recieve current date time but only in number/raw, then using `intl` package to reformat it as you like. For example DateTime.now() will be reformat with DateFormat.MMMMd().format(DateTime.now()) for MMMMd is the skeleton format 

- MMMMd is 'month' 'day(in number)' / April 8

For more DateFormat skeleton you can visit this api [documentation](https://api.flutter.dev/flutter/intl/DateFormat-class.html) 

```
1. method 1 general
var dateTimeRaw = DateTime.now();
String dateTime = DateFormat.MMMMd().format(dateTimeRaw);

2. method 2 / i like this more :D
String dateTime = DateFormat.MMMMd().format(DateTime.now());
```


<br />


## CRUD, Create Read Update Delete

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


<br />
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

### # Implementing shared_preferences / localstorage
1. In newest flutter initializing the function is a little bit different put it outside the build
```
final Future<SharedPreferences> _prefs = SharedPreferences.getInstance();
```

2. Make a list variable that contain the data which is will appear in the ui + the add data to the list function
```
var noteList = [];

 void addNote(id, note, description) {
    noteList.add({
      'id': id,
      'note': note,
      'description': description,
    });
  }
```

3. Make save data function to store data to localstorage, so from temporary storage that contain `noteList` transferred to new variables `notes` then the new variables will be encode and saved to the localstorage with keys `notes`
```
 Future saveData() async {
    final SharedPreferences prefs = await _prefs;
    
    List notes = noteList;
    prefs.setString('notes', jsonEncode(notes));
  }
```

4. Load the data from localstorage, if prefs/preferences/localstorage contains key `notes`(keys that we store before) then the key data will be transferred to the variables in temporary storage `_noteList` then the decode the `_noteList` and save it to new variables, now we have variables `notes` list that contains all the data now we will looping it and pass every item in it to our first list/main list that will contain the data to show in the ui.
```
Future loadData() async {
    final SharedPreferences prefs = await _prefs;
    
    if (prefs.containsKey('notes')) {
      final _noteList = prefs.getString('notes');
      final notes = jsonDecode(_noteList!);
      for (var i = 0; i < notes.length; i++) {
        noteList.add(notes[i]);
        setState(() {});
      }
    }
  }
```

5. To remove the selected data from localstorage is a little bit tricky, when we tap the delete icon in spesific/selected item we will do this. first we delete the item data from temporary sotrage list `noteList` then clear/remove the keys `notes` from localstorage after that the keys is removed and the new temporary sotrage list `noteList` is without the data that we deleted before now save the list again to localstorage. 
It's simply like delete selected data list and the keys then save the new list without the selected data and save it again to keys
```

  Future deleteData() async {
    final SharedPreferences prefs = await _prefs;

    prefs.clear();
    saveData();
  }

```
