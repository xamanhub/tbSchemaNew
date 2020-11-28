# 表单属性和控件
## 一、属性
* `realtimeSave`:实时保存
* `type`:控件类型
* `dataName`:数据名称
  * 在取数据时props.mds.moduleData.dataName
* `invisible`:控件不可见
  * bool类型 false为可见，true为不可见
* `label`:控件标签 
  * `description`:标签描述
    * `icon`:图标描述
    * `desc`:文字描述
  * `title`:标签标题
* `validateProps`:控件验证规则
  * `dataType`:数据类型
  * `required`:是否必填
  *  `validate`:是否验证填写数据类型和dataType类型匹配
* `style`:控件样式
* `wrapperStyle`:整个控件容器的样式
* `extension`:扩展属性(每种控件扩展属性都有区别)
  * `relateData`:如需跳转其他页面地址操作  需要携带的数据  如需其他控件的数据 使用控件id.dataName
  * `dialogType`:跳转其他页面时打开方式  dialog(弹窗)
  * `sendDataType`:打开的弹窗是否展示内容  只要不为空字符串 都是true
  * `url`:打开的弹窗展示内容地址
  * `defaultValue`:默认值
  * `dataSource`:数据选择源 数组类型
  * `limitHeight`:当控件是image时 是否保持上传的图片尺寸必须和第一张相同
  * `multiple`:是否显示多行
  * 。。。。。

## 二、rules  相当于if else 判断来更改控件属性值 常用于控制 控件的显示与隐藏
* `conditio`:匹配规则 
* `components`:参与的组件
  * 组件id:{
  	属性:值
  }
  * 例：
```json
"rules": [{
		"condition": "${moduleData.mode}==1",
		"components": {
			"arrayConSetting": {
				"invisible": false
			},
			"otherSetting": {
				"invisible": true
			}
		},
		"desc": ""
	},
	{
		"condition": "${moduleData.mode}==2",
		"components": {
			"arrayConSetting": {
				"invisible": true
			},
			"otherSetting": {
				"invisible": false
			}
		},
		"desc": ""
	}
]
```

## 三、layout 布局 控件的排列顺序
* 例： 
```json
"layout": [{
		"children": [
			"pageImage",
			"pageLink"
		],
		"root": true,
		"id": "1510911008848_3"
	},
	{
		"children": [],
		"root": false,
		"id": "pageImage"
	},
	{
		"children": [],
		"root": false,
		"id": "pageLink"
	}
]
```

**必须有一个控件的root属性为true，通常有Map、Container等可以包含子控件的**

## 四、控件
### 1、Container控件 容器组件，该组件没有任何功能
```json
"ContainerID": {
	"wrapperStyle": {
		"height": "10px"
	},
	"invisible": false,
	"style": {
		"width": "auto",
		"height": "auto"
	},
	"label": {
		"description": "",
		"title": ""
	},
	"type": "OfficialContainer"
}
```

### 2、Input控件  输入框组件
* `multiple`：是否显示多行
* `max`：最多输入字符数，不写为无限
```json
"InputID": {
	"extension": {
		"useReg": false,
		"multiple": true,
		"placeholder": "请输入关键字"
	},
	"wrapperStyle": {},
	"dataName": "text_content",
	"style": {
		"width": "auto",
		"height": "auto"
	},
	"label": {
		"description": {
			"icon": "",
			"desc": ""
		},
		"title": "文本内容"
	},
	"type": "OfficialInput",
	"validateProps": {
		"max": 100.0,
		"dataType": "Text",
		"required": true,
		"validate": true
	}
}
```

### 3、InteractVideo控件  上传视频组件
```json
"InteractVideoID": {
	"extension": {},
	"wrapperStyle": {},
	"dataName": "videoInfo",
	"style": {},
	"label": {
		"description": {
			"icon": "",
			"desc": "支持商品小卡、优惠券、红包等在视频上展现视频最小尺寸640x360，长度2分钟以内"
		},
		"title": "选择互动视频"
	},
	"type": "OfficialVideo",
	"validateProps": {
		"dataType": "Map",
		"required": true,
		"validate": true
	}
}
```

### 4、Range控件   数字区间组件
```json
"RangeID": {
	"extension": {
		"dataMap": {
			"start": "startPrice",
			"end": "endPrice"
		},
		"startText": "过滤价格",
		"placeholder": "￥",
		"endText": "元"
	},
	"wrapperStyle": {},
	"dataName": "filterPrice",
	"style": {
		"width": "auto",
		"height": "auto"
	},
	"label": {
		"description": {
			"icon": "",
			"desc": ""
		},
		"title": ""
	},
	"type": "OfficialRange",
	"validateProps": {
		"dataType": "Map",
		"required": false,
		"validate": false
	}
}
```

### 5、Skip控件   跳转链接组件    ---没试过
* `url`：跳转地址
```json
"SkipID": {
	"extension": {
		"text": "新建分类",
		"url": "//siteadmin.tmall.com/category/index.htm"
	},
	"wrapperStyle": {
		"marginTop": "-10px"
	},
	"dataName": "skip",
	"style": {
		"width": "auto",
		"height": "auto"
	},
	"label": {
		"description": {
			"icon": "",
			"endIcon": "arrow-double-right",
			"desc": ""
		},
		"title": ""
	},
	"type": "OfficialSkip",
	"validateProps": {
		"dataType": "",
		"required": false,
		"validate": false
	}
}
```

### 6、SingleImage组件  上传图片组件
* `dele`:选择后是否可以删除图片
* `limitHeight`:图片尺寸是否必须一致
* `needCrop`:选择图片后是否需要剪裁
```json
"SingleImageID": {
	"extension": {
		"dialogType": "dialog",
		"relateData": "wigete_id",
		"sendDataType": "url",
		"dele": true,
		"moduleType": "single_image",
		"limitHeight": false,
		"text": "添加图片",
		"config": {
			"minHeight": 0,
			"maxHeight": 1500,
			"mime": "jpg,png",
			"needCrop": false,
			"minWidth": 0,
			"type": "pic",
			"maxWidth": 750
		},
		"url": "//sucai.wangpu.taobao.com/select.htm"
	},
	"wrapperStyle": {
		"paddingBottom": "4px"
	},
	"invisible": false,
	"dataName": "pic",
	"style": {
		"width": "auto",
		"height": "90px"
	},
	"label": {
		"description": {
			"icon": "",
			"desc": ""
		},
		"title": "轮播主图"
	},
	"type": "TaobaowpSingleImage",
	"validateProps": {
		"dataType": "Image",
		"required": false,
		"validate": false
	}
}
```

### 7、Select组件  下拉框组件
```json
"selectID": {
	"extension": {
		"defaultValue": 1,
		"placeholder": "请选择人群数量",
		"dataSource": [{
				"label": "1",
				"value": 1
			},
			{
				"label": "2",
				"value": 2
			},
			{
				"label": "3",
				"value": 3
			},
			{
				"label": "4",
				"value": 4
			},
			{
				"label": "5",
				"value": 5
			}
		]
	},
	"wrapperStyle": {
		"paddingBottom": "20px",
		"borderBottom": "1px solid #E1E1E1",
		"marginTop": "20px"
	},
	"invisible": false,
	"dataName": "crowd_count",
	"style": {
		"width": "auto",
		"height": "auto"
	},
	"label": {
		"description": {
			"icon": "",
			"desc": "请选择需要添加的人群数量"
		},
		"title": "人群数量"
	},
	"type": "OfficialSelect",
	"validateProps": {
		"dataType": "",
		"required": false,
		"validate": false
	}
}
```

### 8、Map组件  
* 和Container一样没有功能，只能当做容器使用
* 和Containe的不同：
  * 他自己有layout ，不需要再最外的layout写
```json
"MapID": {
	"layout": [],
	"components": {
	},
	"wrapperStyle": {
		"marginBottom": "15px",
		"borderBottom": "1px solid #E1E1E1"
	},
	"dataName": "custom_1",
	"type": "OfficialMap",
	"validateProps": {
		"required": false,
		"validate": true
	}
}
```

### 9、Radio组件    单选框组件  有两种展示效果
* 按钮效果：当`style`属性里的width设置了值时，显示为按钮效果
```json
"RadioID1": {
	"extension": {
		"confirm": {},
		"shape": "button",
		"size": "medium",
		"defaultValue": "1",
		"type": "",
		"dataSource": [{
				"label": "通用模式",
				"value": "1"
			},
			{
				"label": "人群模式",
				"value": "2"
			}
		]
	},
	"wrapperStyle": {
		"marginTop": 0
	},
	"invisible": false,
	"dataName": "mode",
	"style": {
		"margin": "0 auto",
		"width": "185px"
	},
	"label": {
		"description": {
			"icon": "",
			"desc": ""
		},
		"title": ""
	},
	"type": "OfficialRadio",
	"validateProps": {
		"dataType": "Text",
		"required": false,
		"validate": false
	}
}
```
* 普通单选圈圈：当`style`属性里的height和width都为auto时，显示为普通的单选圈圈效果
```json
"RadioID2": {
	"extension": {
		"confirm": {},
		"shape": "",
		"size": "large",
		"defaultValue": "2",
		"type": "",
		"dataSource": [{
				"label": "是",
				"value": "1"
			},
			{
				"label": "否",
				"value": "2"
			}
		]
	},
	"wrapperStyle": {},
	"invisible": false,
	"dataName": "isUntouch",
	"style": {
		"width": "auto",
		"height": "auto"
	},
	"label": {
		"description": {
			"icon": "",
			"desc": ""
		},
		"title": "是否禁止滑动"
	},
	"type": "OfficialRadio",
	"validateProps": {
		"dataType": "Number",
		"required": false,
		"validate": false
	}
}
```
### 10、Link组件    链接选择组件
```json
"LinkID": {
	"extension": {
		"config": {},
		"url": "//siteoperateplatform.taobao.com/open/link"
	},
	"wrapperStyle": {
		"paddingBottom": "4px"
	},
	"invisible": false,
	"dataName": "url",
	"style": {
		"width": "auto",
		"height": "auto"
	},
	"label": {
		"description": {
			"icon": "link",
			"desc": "轮播点击链接"
		},
		"title": ""
	},
	"type": "OfficialLink",
	"validateProps": {
		"dataType": "Link",
		"required": false,
		"validate": false
	}
}
```
### 11、Array组件   
* 该组件只会显示`components`的一个组件
* `components`中需放多个组件时,需要加Map，再在Map组件中放入需要的组件
```json
"arrayID": {
	"components": {},
	"dataName": "array",
	"extension": {
		"defaultValue": true,
		"placeholder": "placeholder",
		"useReg": false
	},
	"invisible": false,
	"label": {
		"description": {
			"desc": "数组",
			"icon": ""
		},
		"title": "数组"
	},
	"layout": [{
		"children": [],
		"id": "1597821517787_1",
		"root": true
	}],
	"style": {
		"height": "auto",
		"width": "auto"
	},
	"type": "OfficialArray",
	"validateProps": {
		"dataType": "Array",
		"max": 6,
		"min": 1,
		"required": false,
		"validate": false
	},
	"wrapperStyle": {}
}
```
