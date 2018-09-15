## ARM 编译器中的 VFP 支持

ARM 编译器完全支持 VFP 的使用\(尽管一些构建可以默认配置为不支持 VFP，在这种情况下浮点计算将使用库代码\)

ARM 编译器中 VFP 支持的主要可选是：

* --fpu=name that lets you specify the target floating-point hardware

其他选项可用于指定对 ARM Cortex-A 系列处理器上的特定 VFP 实现的支持：

* --fpu=vfpv3 or --fpu=vfpv3\_d16 \(for the Cortex-A8 and Cortex-A9 processors\)
* --fpu=vfpv4 or --fpu=vfpv4\_d16 \(for all other Cortex-A series processors\)

这些选项可以用于只在这些 VFP 实现上运行的代码，并且不需要向后兼容旧的 VFP 实现。使用 --fpu=list 查看支持的 FPU 的完整列表。

以下选项可用于链接支持：

* --apcs=/hardfp generates code for hardware floating-point linkage
* --apcs=/softfp generates code for software floating-point linkage

硬件浮点链接使用 FPU 寄存器来传递参数和返回值。软件浮点链接意味着函数的参数和返回值是通过 ARM 整数寄存器 R0 和堆栈来传递的。--apcs=/hardfp 和 --apcs=/softfp 与 --fpu 的显式或隐式使用交互或覆盖。

