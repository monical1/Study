> 定义枚举类
```groovy
enum FileStatus {

    qr("已迁入","qr"),
    qc("已迁出","qc"),
    tx("已退休","tx"),
    sw("已死亡","sw"),
    qt("其他","qt")

    private String name
    private String value

    FileStatus(String name,String value) {
        this.name = name
        this.value = value
    }


    @Override
    public String toString() {
        return this.name
    }
}
```
> 使用说明
```groovy
//同时获取键值
FileStatus.collect{[name:it.name,value:it.value]}

//字符转枚举对象
def fs = FileStatus.valueOf(value)
fs.name
fs.value

//值集合
FileStatus.values().toList()

```
