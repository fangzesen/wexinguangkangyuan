# 表单联动和日期计算json说明

* [1. 表单联动](#1)
  * [toggle](#2)
  * [select](#3)
* [2. 日期计算](#4)
* [3. 整体json](#5)

***

## 1. 表单联动 {#1}

### toggle {#2}

```json
{
    "txt": "显示关联时间",
    "value": true,
    "type": "radio",
    "extend": {
        "field": "REC_JCGCDY",
        "fieldtype": "",
        "enumeration": [],
        "relateList": [
            "REC_QJKSSJY",
            "REC_QJJSSJY",
            "REC_GLZJ"
        ]
    }
}
```

1. `value`字段是否是**布尔型**？能否具有**初始值**？
2. `extend`中的`relateList`表示关联的其它字段的**标志属性数组**

### select {#3}

```json
{
    "txt": "请假类型",
    "value": "",
    "type": "select",
    "extend": {
        "field": "REC_QJLX",
        "editable": "False",
        "fieldtype": "",
        "enumeration": [{
            "key": "290006",
            "value": "休假"
        }, {
            "key": "290001",
            "value": "事假"
        }, {
            "key": "290003",
            "value": "探亲假"
        }, {
            "key": "290099",
            "value": "其他"
        }]
    }
}
```

1. 如果需要根据选的类型加载**二级表单**，对应的**键值表**应该如何设置？

## 2. 日期计算 {#4}

```json
{
    "txt": "",
    "value": "",
    "type": "date",
    "extend": {
        "field": "REC_QJKSSJ",
        "fieldtype": "",
        "enumeration": [],
        "dateArray": [{
            "txt": "请假起始时间-详细",
            "value": "",
            "type": "dateyymm",
            "extend": {
                "field": "REC_QJQSSJ",
                "fieldtype": "start",
                "enumeration": []
            }
        }, {
            "txt": "请假结束时间-详细",
            "value": "",
            "type": "dateyymm",
            "extend": {
                "field": "REC_QJJSSJ",
                "fieldtype": "end",
                "enumeration": []
            }
        }, {
            "txt": "总计-改",
            "value": "",
            "type": "text",
            "extend": {
                "field": "REC_ZJ",
                "fieldtype": "interval",
                "enumeration": []
            }
        }]
    }
```

1. `"type": "date"`表示一组**日期集**（包含日期、文本字段）
2. `extend`中的`dateArray`表示日期集的具体**字段数组**。其中，这些**字段**需要一个属性表示在运算关系中的**地位**，目前假设为`fieldtype`
3. **跨字段校验**的规则能否仅用**地位**属性实现？
4. **特殊计算**的规则（如计算请假天数，除了法定节假日，有无可能存在企业后台设置的特殊加班日？）怎么定义？

## 3. 整体json {#5}

```json
[{
    "txt": "请假类型",
    "value": "",
    "type": "select",
    "extend": {
        "field": "REC_QJLX",
        "editable": "False",
        "fieldtype": "",
        "enumeration": [{
            "key": "290006",
            "value": "休假"
        }, {
            "key": "290001",
            "value": "事假"
        }, {
            "key": "290003",
            "value": "探亲假"
        }, {
            "key": "290099",
            "value": "其他"
        }]
    }
}, {
    "txt": "显示关联时间",
    "value": true,
    "type": "radio",
    "extend": {
        "field": "REC_JCGCDY",
        "fieldtype": "",
        "enumeration": [],
        "relateList": [
            "REC_QJKSSJY",
            "REC_QJJSSJY",
            "REC_GLZJ"
        ]
    }
}, {
    "txt": "关联起始时间",
    "value": "",
    "type": "dateyymmdd",
    "extend": {
        "field": "REC_QJKSSJY",
        "fieldtype": "",
        "enumeration": []
    }
}, {
    "txt": "关联结束时间",
    "value": "",
    "type": "dateyymmdd",
    "extend": {
        "field": "REC_QJJSSJY",
        "fieldtype": "",
        "enumeration": []
    }
}, {
    "txt": "关联总计",
    "value": "",
    "type": "text",
    "extend": {
        "field": "REC_GLZJ",
        "fieldtype": "float",
        "enumeration": []
    }
}, {
    "txt": "",
    "value": "",
    "type": "date",
    "extend": {
        "field": "REC_QJKSSJ",
        "fieldtype": "",
        "enumeration": [],
        "dateArray": [{
            "txt": "请假起始时间-改",
            "value": "",
            "type": "dateyymmdd",
            "extend": {
                "field": "REC_QJQSSJ",
                "fieldtype": "start",
                "enumeration": []
            }
        }, {
            "txt": "请假结束时间-改",
            "value": "",
            "type": "dateyymmdd",
            "extend": {
                "field": "REC_QJJSSJ",
                "fieldtype": "end",
                "enumeration": []
            }
        }, {
            "txt": "总计-改",
            "value": "",
            "type": "text",
            "extend": {
                "field": "REC_ZJ",
                "fieldtype": "interval",
                "enumeration": []
            }
        }]
    }
}, {
    "txt": "",
    "value": "",
    "type": "date",
    "extend": {
        "field": "REC_QJKSSJ",
        "fieldtype": "",
        "enumeration": [],
        "dateArray": [{
            "txt": "月份-不需要运算仅显示",
            "value": "",
            "type": "datetime",
            "extend": {
                "field": "REC_QJQSSJ",
                "fieldtype": "",
                "enumeration": []
            }
        }]
    }
}, {
    "txt": "",
    "value": "",
    "type": "date",
    "extend": {
        "field": "REC_QJKSSJ",
        "fieldtype": "",
        "enumeration": [],
        "dateArray": [{
            "txt": "请假起始时间-详细",
            "value": "",
            "type": "dateyymm",
            "extend": {
                "field": "REC_QJQSSJ",
                "fieldtype": "start",
                "enumeration": []
            }
        }, {
            "txt": "请假结束时间-详细",
            "value": "",
            "type": "dateyymm",
            "extend": {
                "field": "REC_QJJSSJ",
                "fieldtype": "end",
                "enumeration": []
            }
        }, {
            "txt": "总计-改",
            "value": "",
            "type": "text",
            "extend": {
                "field": "REC_ZJ",
                "fieldtype": "interval",
                "enumeration": []
            }
        }]
    }
}]
```
