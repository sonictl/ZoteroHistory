# ZoteroHistory

## Never get lost! Add a history feature for paper jumping in Zotero!

I often get lost when jumping between papers. After jumping from paper A to paper B, I am unable to go back to paper A if I forget its title.

I want an extension to add a history feature for paper viewing in Zotero. I didn't find a way to build extension (how to generate a .zoteroplugin from source code?) for Zotero 5.0 in the official documentation. And I failed at compiling and installing the the source code for the hello-world-zotero extension, on Zotero 5.0.

Fortunately, with Zotero 5.0's javascript API, I've managed to manually log the paper view history in Zotero. It's not quite user friendly yet, but it barely works.

Tell me if you have better methods!

### Test environment:

 - Zotero v5.0.87
 - tested on Mac OSX 10.15.4
 - windows user can try the same way and comment on how it works. thx!

### Useage:

```
`Zotero` -> `Tools` -> `Develop` -> `Run javascript`
```

**step1:** Initialize the variable by executing the first patch of code:

```javascript
//=== initialize the history ====
var items = Zotero.getActiveZoteroPane().getSelectedItems();
var cur_itemKey = items[0].key;
var tmp_key = cur_itemKey;
var key_paper_list = 'List of keys of papers your selected:\n';
cur_itemKey += '\n';
```

**step2:** Then replace the first patch of code with the below.

```javascript
//==== run above once, and modify above 5 lines into: ====
items = Zotero.getActiveZoteroPane().getSelectedItems();
cur_itemKey = items[0].key + '\n';
if(items[0].key !=tmp_key){
	tmp_key = items[0].key;
	key_paper_list += cur_itemKey;
}
else{
    key_paper_list += '';
}
```

**step3:** Return to the Zotero main screen and browse papers. Return javascript interface and run once the 2nd code patch every time you switch papers. The javascript interface executes the code once to log a view history.

**step4:** You can go back through the browsing history by searching and entering the key directly.

## Tips:

on Mac OSX, use `Command`+` to switch between javascript running interface and Zotero paper viewing interface.
