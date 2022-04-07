# code-documentation

<br />

#### # Remove Item
>1. This will remove item that are picked from looping/item builder index
```
 item.removeAt(id);
```


#### # Remove Item
>1. This will remove item that are picked from looping/item builder index, i is the index from looping/item builder
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

>2. This will remove item if the item id is the same as the item id that are select/item that pressed to be remove
```
item.removeWhere(
      (element) => element.id == id,
    );
```
