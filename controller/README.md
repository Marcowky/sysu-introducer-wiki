# 控制器

本系统提供 `CLI` 和 `Webui` 两种控制器，供管理员使用。
其中前者主要针对系统的开发者，便于他们在本地进行调试，
后者则面向实际的使用场景，
通过提供图形化的交互页面，
保证不了解系统底层原理的人也能够对数字人系统进行简单管理控制。

控制器包括**模块控制**、**消息交互**和**系统配置**3 个功能。

## 模块控制

模块控制功能包括启动和停止系统中的各个模块，具体包括如下功能。

-   控制模块运行
-   查看模块信息 `ModuleInfo`
-   修改模块的配置信息 `Config`
-   修改模块的实现类型 `kind`

### 1. 控制模块运行

控制模块运行是指启动和停止模块，
目前本系统支持控制的模块只有 `booter` 和与其子模块（不包括嵌套的子模块），
这些模块我们定义为**可控模块**（Controllable Module），
除此之外的所有模块都不能由管理员进行单独控制，
其运行阶段的生命周期由其父模块决定。

`booter` 模块对于整个系统而言属于组织者，
换句话说，其本身并不提供实质上的功能，
而是负责牵动其子模块的运行。
在控制器的角度来看，
对`booter`的控制指令实际上类似于控制脚本，
也就是说 `booter` 的状态与其子模块模块无关。
管理员可以单独控制这些可控模块，不会影响 `booter` 模块的状态，
而控制 `booter` 模块的启动和停止，
则会一键控制所有可控模块的启动和停止。

> 以上控制逻辑的设计主要是避免给系统引入过多地状态和复杂度。

### 2. 查看模块信息

查看模块信息是指显示模块对应 `ModuleInfo` 中的属性信息，
该对象包含的属性较多，其中可以通过控制器查看的属性由**可见性**决定，
其具体属性可以查看[模块化部分](../structure/modular.md)的文档。

### 3. 修改模块的配置信息

管理员可以通过控制器直接修改模块对应的配置信息，
但值得注意的是，管理员只能修改已经存在的配置，
不支持动态地添加和删除配置信息内容，
且模块的类型（`boolean`/`number`/`string`）不支持动态改变。

除此之外，正如[配置文件](../structure/config.md)部分提到的，
模块的配置信息在运行时保持不变的，
因此管理员不能在模块运行时对其进行修改。

### 4. 修改模块的实现类型

模块的配置信息对应模块的运行阶段，
而实现类型对应的模块的加载阶段。
系统在初始化阶段，会根据 `modules.json` 中的配置信息，
加载默认的实现类型。
此后，当模块停止后，管理员也可以在后续修改对应的实现类型。

## 消息交互

> TODO: ...

<!-- ## 账号管理

控制器内部包含一个简单的数据库，用于控制管理员的账号，以及授权访问。
其中管理员分为根管理员，和普通管理员，
前者是系统初始时包含的管理员，后续该根管理员可以创建其他管理员，
一起协同管理和运营数字人。

> TODO: 属于额外部分，可等待后续进行开发 -->
