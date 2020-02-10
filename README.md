# 编写前端代码标准  
npm 引入方式标准   
10.不许使用var变量声明   
20.禁止使用setInterval    
30.禁用eval  
40.自定义函数，参数不得超过两个，参数中不要使用回调函数（除非回调函数需要多次运行，例如XMLHttpRequest的进度回调函数），Promise替代，防止地狱回调  
50.除独立的库，不要重复定义同样功能的函数  
60.语言包要独立，不允许每个文件出现文字字符，全部包含到一处（例如中文语言包，英文语言包）

FileReader的Promise写法
```
const toFileReader = (file,methods) => {
    const readmethods=({DataURL:"readAsDataURL",ArrayBuffer:"readAsArrayBuffer",BinaryString:"readAsBinaryString",readAsText:"readAsText"})[methods]||"readAsDataURL";

    return new Promise((resolve, reject)=>{

        const reader = new FileReader();
        reader.onload = res => {
            resolve(res.target.result);
        };
        (reader[readmethods])(file);
        reader.onerror = error => reject(error);
    })
}
```
代替eval 
```
const evil = fn => {
    return new Function("return " + fn)();
}
```
