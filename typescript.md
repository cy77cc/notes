# typescript

## 基础数据类型

```typescript
布尔型
let isBool: boolean = true;
数字型
let num: number = 20;
let hexLiteral: number = 0xf00d; 十六进制
let binaryLiteral: number = 0b1010; 二进制
let octalLiteral: number = 0o744; 八进制
字符串
let name: string = "张三";
let name: string = `Hello, ${name}`; 模板字符串
数组
let list: number[] = [1, 2, 3, 4, 5];
let list: Array<string> = ["a", "b", "c"];  使用泛型定义
元组
let x: [number, string] = [10, 'name'];
console.log(x[0]); // 10
console.log(x[1]); // name
枚举类型 类似数组
默认索引是从0开始，可以自己赋值
enum Color {
    Red = 1,  从1开始 也可以对每个项赋一个索引
    Green,
    Yellow,
}
let c: Color = Color.Red; c=1
let str3: string = Color[1];  通过索引获取对应的元素
console.log(str3);// Red
any类型 定义不确定的类型 可以调用没有定义的方法编译时不会报错
let notSure: any = 4;
notSure.push();
notSure = "maybe a string noSure";
notSure = false;
console.log(typeof(notSure)); // boolean
let list: any[] = [1, "name"]; 定义一个不确定类型的数组
void空类型
undefined和null类型
never
never类型表示的是那些永不存在的值的类型
Object非原始类型
```

