# makefile_template
便于移植的makefile模板

## 介绍
这是 makefile 模板，支持`gcc`和`arm-none-eabi-gcc`两种编译器，只需要修改**少量**文件就能移植。

### 目录结构
通俗地说，`makefile`是主驱动，`makefile.build`是通用的规则和工具，`build.mk`则是数据。

```
.
├── app
│   ├── b.c
│   ├── build.mk
│   └── main.c
├── build.mk
├── component
│   ├── build.mk
│   └── mt.c
├── drv
│   ├── build.mk
│   ├── c.c
│   └── led
│       ├── build.mk
│       └── d.c
├── include
│   └── demo.h
├── lib
│   ├── build.mk
│   └── hal_drv
│       ├── inc
│       └── src
│           └── e.c
├── Makefile
├── Makefile.build
└── readme.md
```

### 许可证
makefile_template 遵循 LGPLV2.1 许可，详见`LICENSE`文件。

### 版本日志
- v1.0
	- makefile 初版

## 如何使用

### 移植到新的工程，哪些文件需要修改？
- `build.mk`
- `makefile`

### `build.mk`如何添加文件、目录？
`build.mk` 的作用是添加**要编译**的文件，那么如果目录存在嵌套呢？

- 如何添加`main.c`？（`.s`, `.S`也是一样的做法）
	- `obj-y += main.o`
	> 注意：写的是`.o`

- 如何添加`demo.h`？
	- `CCFLAGS += -I$(src)/include`

- 如何添加目录？
	- `obj-y += tuzi/`
	> **注意：`tuzi`后面的`/`一定不能漏掉！！！**

### 何时需要添加`build.mk`？
- 如果想方便看清目录结构
	- 例如ipc组件，内存管理组件，有各自的`build.mk`

- 如果此目录的内容，想比较方便地增删
	- 例如驱动组件

### 何时不需要添加`build.mk`？
- 添加库
	- 例如上面目录结构的`lib/`

> 总的来说，整个工程里`build.mk`可以只有一个，也可以有多个，只要能清晰划分组件结构以及方便增删就可以了。

### `makefile`如何修改？
`makefile`里的`CCFLAGS`、`ASFLAGS`、`LDFLAGS`参数根据具体的需求修改
