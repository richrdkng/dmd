<a name="module_file-set"></a>
##file-set
Exports a contructor taking a list of file patterns as input, returning a `file-set` instance containing the expanded patterns split into separate lists of `files`, `dirs` and `notExisting`.

**Example**  
```js
var fileSet = require("file-set");
```

* [file-set](#module_file-set)
  * [class: FileSet](#exp_module_file-set--FileSet) ⏏
    * [new FileSet(patternList)](#new_module_file-set--FileSet_new)
    * _instance_
      * [.list](#module_file-set--FileSet#list) → <code>Array.&lt;string&gt;</code>
      * [.files](#module_file-set--FileSet#files) → <code>Array.&lt;string&gt;</code>
      * [.dirs](#module_file-set--FileSet#dirs) → <code>Array.&lt;string&gt;</code>
      * [.notExisting](#module_file-set--FileSet#notExisting) → <code>Array.&lt;string&gt;</code>
      * [.add(files)](#module_file-set--FileSet#add)
    * _static_
      * [enum: .eFileType](#module_file-set--FileSet.eFileType) → <code>number</code>
        * [.NOEXIST](#module_file-set--FileSet.eFileType.NOEXIST) → <code>number</code>
        * [.FILE](#module_file-set--FileSet.eFileType.FILE) → <code>number</code>
        * [.DIR](#module_file-set--FileSet.eFileType.DIR) → <code>number</code>

<a name="exp_module_file-set--FileSet"></a>
###class: FileSet ⏏
Expands file patterns, returning the matched and unmatched files and directories

<a name="new_module_file-set--FileSet_new"></a>
####new FileSet(patternList)
| Param | Type | Description |
| ----- | ---- | ----------- |
| patternList | <code>string</code> \| <code>Array.&lt;string&gt;</code> | A pattern, or array of patterns to expand |

<a name="module_file-set--FileSet#list"></a>
####fileSet.list → <code>Array.&lt;string&gt;</code>
The full list of unique paths found, and not found.

<a name="module_file-set--FileSet#files"></a>
####fileSet.files → <code>Array.&lt;string&gt;</code>
The existing files found

<a name="module_file-set--FileSet#dirs"></a>
####fileSet.dirs → <code>Array.&lt;string&gt;</code>
The existing directories found

<a name="module_file-set--FileSet#notExisting"></a>
####fileSet.notExisting → <code>Array.&lt;string&gt;</code>
Paths which were not found

<a name="module_file-set--FileSet#add"></a>
####fileSet.add(files)
add file patterns to the set

| Param | Type | Description |
| ----- | ---- | ----------- |
| files | <code>string</code> \| <code>Array.&lt;string&gt;</code> | A pattern, or array of patterns to expand |

<a name="module_file-set--FileSet.eFileType"></a>
####enum: FileSet.eFileType → <code>number</code>
Enum for the `type` value of each record in `fileSet.list`

**Properties**

| Name | Type | Description |
| ---- | ---- | ----------- |
| NOEXIST | <code>number</code> | when a file doesn't exist |
| FILE | <code>number</code> | It's a file |
| DIR | <code>number</code> |  |

**Properties**: `NOEXIST`, `FILE`, `DIR`  
**Read only**: true  

* [enum: .eFileType](#module_file-set--FileSet.eFileType) → <code>number</code>
  * [.NOEXIST](#module_file-set--FileSet.eFileType.NOEXIST) → <code>number</code>
  * [.FILE](#module_file-set--FileSet.eFileType.FILE) → <code>number</code>
  * [.DIR](#module_file-set--FileSet.eFileType.DIR) → <code>number</code>

<a name="module_file-set--FileSet.eFileType.NOEXIST"></a>
#####eFileType.NOEXIST → <code>number</code>
when a file doesn't exist

**Default**: `0`  
<a name="module_file-set--FileSet.eFileType.FILE"></a>
#####eFileType.FILE → <code>number</code>
It's a file

**Default**: `1`  
<a name="module_file-set--FileSet.eFileType.DIR"></a>
#####eFileType.DIR → <code>number</code>
**Default**: `2`  