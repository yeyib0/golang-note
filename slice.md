# 数据结构
```
type SliceHeader struct {
	Data uintptr
	Len  int
	Cap  int
}
```
# 创建
```
// 使用数组或者切片的一部分
arr := [3]int{1,2,3}
sli := arr[:1]

// 使用字面量
[]int{}

// 使用make关键字
make([]int, 1, 1)
```
# 访问元素
# 扩容
# 拷贝
切片长度可变，内存分配可变，具有容量，参数传递时传递引用
