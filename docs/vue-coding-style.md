## Vue项目开发规则
适用的开发语言：TypeScript/Vue
代码文件扩展名：.vue

### 代码文件要求
- 组件文件命名使用kebab-case风格。
- 组件文件应当放在components文件夹下，组件文件同名的文件夹下，如：组件文件名为text-input.vue，组件文件存放路径为components/text-input/text-input.vue。

### 代码编写要求
1. 每行代码不要超过240个英文字符。
2. 函数参数定义时，优先在一行内定义，超出240个英文字符时，按参数定义为单元进行换行。

### 代码结构要求
- 组件定义时，要遵循以下代码块顺序：
1. 模板代码
2. 脚本代码
3. 脚本代码-静态常量，静态常量定义顺序为：
	1. readonly常量
	2. defineProps，属性定义，注意要使用defineProps<泛型类型>的方式定义，明确属性类型，属性没有明确指定时，都为可为未定义的类型，如：
	```
	defineProps<{
		userName?:string,
		userAge?:number
	}>();
	```
	3. defineModel，双向绑定属性定义，注意要使用defineProps<泛型类型>的方式定义，明确属性类型，属性没有明确指定时，都为可为未定义的类型。
	4. provide，注入定义。
	5. defineExpose，方法暴露。
	6. defineEmits，事件定义，注意需要在defineEmits前定义事件名称常量，如：
	```
	const EventName_DidGotFocus = "didGotFocus";
	const EventName_DidLoseFocus = "didLoseFocus";
	const _emits = defineEmits([
	    EventName_DidGotFocus,
	    EventName_DidLoseFocus]);
	```
	5. onEvent，事件关联，如：
	```
	onMounted(didLoad);
	```
	
4. 脚本代码-自身属性，自身属性定义顺序为：
	1. 通用底层属性，如当前App对象。
	2. 当前组件其他属性，属性定义顺序应当按依赖关系，从底层到上层定义。
5. 脚本代码-类方法
6. 脚本代码-私有方法
7. 脚本代码-事件节点
8. 所有脚本代码的代码块都要使用如下格式的注释进行分隔，方便阅读代码时定位跳转：
```
////////////////////////////////////////////////  
// @当前代码块名称
////////////////////////////////////////////////

#region 当前代码块名称

当前代码块代码

#endregion 
```
9. Ui组件使用规范：
	1. 使用“bx-text-input”时，“placeholder”属性为必填项，文案必须以“请您填写”开头。