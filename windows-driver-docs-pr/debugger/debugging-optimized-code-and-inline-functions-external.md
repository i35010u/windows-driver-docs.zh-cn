---
title: 调试优化的代码和内联函数
description: 对于 Windows 8，调试器和 Windows 编译器已经过增强，因此可以调试优化的代码和调试内联函数。
keywords:
- 调试优化的代码
- 调试内联函数
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 98ac17fe531908e46e2e80ffd3fc44292a205377
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817490"
---
# <a name="debugging-optimized-code-and-inline-functions"></a>调试优化的代码和内联函数


对于 Windows 8，调试器和 Windows 编译器已经过增强，因此可以调试优化的代码和调试内联函数。 调试器将显示参数和局部变量，而不管它们是存储在寄存器中还是存储在堆栈上。 调试器还会在调用堆栈中显示内联函数。 对于内联函数，调试器将显示局部变量而不是参数。

当代码得到优化时，它将转换为运行速度更快，使用的内存更少。 有时会由于删除死代码、合并代码或内联放置函数而删除函数。 还可以删除局部变量和参数。 许多代码优化删除了不需要或使用的局部变量;其他优化将在循环中删除感应变量。 常见的子表达式排除将局部变量合并在一起。

优化了 Windows 的零售版本。 因此，如果您运行的是 Windows 的零售版本，使调试器非常适合与优化代码一起使用非常有用。 为了使优化代码的调试生效，需要两个主要功能： 1) 精确显示本地变量，2) 在调用堆栈上显示内联函数。

## <a name="span-idaccurate_display_of_local_variables_and_parametersspanspan-idaccurate_display_of_local_variables_and_parametersspanspan-idaccurate_display_of_local_variables_and_parametersspanaccurate-display-of-local-variables-and-parameters"></a><span id="Accurate_display_of_local_variables_and_parameters"></span><span id="accurate_display_of_local_variables_and_parameters"></span><span id="ACCURATE_DISPLAY_OF_LOCAL_VARIABLES_AND_PARAMETERS"></span>精确显示局部变量和参数


为了便于精确显示局部变量和参数，编译器会在 (PDB) 文件中记录有关局部变量和参数位置的信息。 这些位置记录跟踪变量的存储位置和这些位置有效的特定代码范围。 这些记录不仅有助于跟踪寄存器或堆栈槽中 (的位置) 变量，还有助于移动变量。 例如，参数可能首先位于 register RCX 中，但移动到堆栈槽以释放 RCX，然后在循环中频繁使用该参数时将其移动到注册 R8，然后在代码超出循环时移到不同的堆栈槽。 Windows 调试器使用 PDB 文件中的丰富位置记录，并使用当前指令指针为本地变量和参数选择适当的位置记录。

Visual Studio 中的 "局部变量" 窗口的此屏幕截图显示优化的64位应用程序中某个函数的参数和局部变量。 函数不是内联函数，因此，我们会看到参数和局部变量。

!["局部变量" 窗口的屏幕截图](images/optimizedcode01.png)

可以使用 [**dv-v**](dv--display-local-variables-.md) 命令查看参数和局部变量的位置。

![显示参数和局部变量位置的屏幕截图](images/optimizedcode02.png)

请注意，"局部变量" 窗口会正确显示参数，即使它们存储在寄存器中也是如此。

除了跟踪具有基元类型的变量外，location 记录还记录本地结构和类的数据成员。 以下调试器输出显示本地结构。

```dbgcmd
0:000> dt My1
Local var Type _LocalStruct
   +0x000 i1               : 0n0 (edi)
   +0x004 i2               : 0n1 (rsp+0x94)
   +0x008 i3               : 0n2 (rsp+0x90)
   +0x00c i4               : 0n3 (rsp+0x208)
   +0x010 i5               : 0n4 (r10d)
   +0x014 i6               : 0n7 (rsp+0x200)

0:000> dt My2
Local var @ 0xefa60 Type _IntSum
   +0x000 sum1             : 0n4760 (edx)
   +0x004 sum2             : 0n30772 (ecx)
   +0x008 sum3             : 0n2 (r12d)
   +0x00c sum4             : 0n0
```

下面是有关上述调试器输出的一些观察值。

-   本地结构 **My1** 说明了编译器可将本地结构数据成员分散到寄存器和非连续堆栈槽。
-   命令 **Dt My2** 的输出将不同于命令 **dt \_ IntSum 0xefa60** 的输出。 不能假设本地结构将占用一个连续的堆栈内存块。 对于 **My2**，仅 `sum4` 保留在原始堆栈块中; 其他三个数据成员移到寄存器。
-   某些数据成员可以有多个位置。 例如， **My2. sum2** 有两个位置：一个是注册 ECX (Windows 调试器选择) ，另一个是 0xefa60 + 0x4 (原始堆栈槽) 。 对于基元类型的局部变量也可能发生这种情况，并且 Windows 调试器会强加引用试探法来确定要使用的位置。 例如，寄存器位置始终为每个堆栈位置。

## <a name="span-iddisplay_of_inline_functions_on_the_call_stackspanspan-iddisplay_of_inline_functions_on_the_call_stackspanspan-iddisplay_of_inline_functions_on_the_call_stackspandisplay-of-inline-functions-on-the-call-stack"></a><span id="Display_of_inline_functions_on_the_call_stack"></span><span id="display_of_inline_functions_on_the_call_stack"></span><span id="DISPLAY_OF_INLINE_FUNCTIONS_ON_THE_CALL_STACK"></span>内联函数在调用堆栈上的显示


在代码优化期间，某些函数会置于行中。 也就是说，函数的主体直接放置在代码中，如宏展开。 没有函数调用，也没有返回调用方。 为了便于显示内联函数，编译器将数据存储在 PDB 文件中，这些文件可帮助对内联函数的代码块进行解码， (也就是说，调用方函数中的代码块序列，这些代码块属于内联) 的被调用方函数，以及这些代码块)  (范围内的局部变量。 此数据可帮助调试器在堆栈展开过程中包括内联函数。

假设你编译一个应用程序，并强制将一个名为的函数 `func1` 内联。

```cpp
__forceinline int func1(int p1, int p2, int p3)
{
   int num1 = 0;
   int num2 = 0;
   int num3 = 0;
   ...
}
```

可以使用 [**bm.exe**](bp--bu--bm--set-breakpoint-.md) 命令在处设置断点 `func1` 。

```dbgcmd
0:000> bm MyApp!func1
  1: 000007f6`8d621088 @!"MyApp!func1" (MyApp!func1 inlined in MyApp!main+0x88)
0:000> g

Breakpoint 1 hit
MyApp!main+0x88:
000007f6`8d621088 488d0d21110000  lea     rcx,[MyApp!`string' (000007f6`8d6221b0)]
```

执行一步后 `func1` ，可以使用 [**k**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 命令 `func1` 在调用堆栈上查看。 您可以使用 [**dv**](dv--display-local-variables-.md) 命令查看的局部变量 `func1` 。 请注意，本地变量 `num3` 显示为 "不可用"。 出于多种原因，本地变量在优化的代码中可能不可用。 这可能是优化代码中不存在该变量。 这可能是因为尚未初始化该变量，或者不再使用该变量。

```dbgcmd
0:000> p
MyApp!func1+0x7:
000007f6`8d62108f 8d3c33          lea     edi,[rbx+rsi]

0:000> knL
# Child-SP          RetAddr           Call Site
00 (Inline Function) --------`-------- MyApp!func1+0x7
01 00000000`0050fc90 000007f6`8d6213f3 MyApp!main+0x8f
02 00000000`0050fcf0 000007ff`c6af0f7d MyApp!__tmainCRTStartup+0x10f
03 00000000`0050fd20 000007ff`c7063d6d KERNEL32!BaseThreadInitThunk+0xd
04 00000000`0050fd50 00000000`00000000 ntdll!RtlUserThreadStart+0x1d

0:000> dv -v
00000000`0050fcb0            num1 = 0n0
00000000`0050fcb4            num2 = 0n0
<unavailable>                num3 = <value unavailable>
```

如果在堆栈跟踪中查看第1帧，可以查看函数的局部变量 `main` 。 请注意，两个变量存储在寄存器中。

```dbgcmd
0:000> .frame 1
01 00000000`0050fc90 000007f6`8d6213f3 MyApp!main+0x8f

0:000> dv -v
00000000`0050fd08               c = 0n7
@ebx                            b = 0n13
@esi                            a = 0n6
```

Windows 调试器聚合 PDB 文件中的数据，以查找内联放置特定函数的所有位置。 您可以使用 [**x**](x--examine-symbols-.md) 命令列出内联函数的所有调用方站点。

```dbgcmd
0:000> x simple!MoreCalculate
00000000`ff6e1455 simple!MoreCalculate =  (inline caller) simple!wmain+8d
00000000`ff6e1528 simple!MoreCalculate =  (inline caller) simple!wmain+160

0:000> x simple!Calculate
00000000`ff6e141b simple!Calculate =  (inline caller) simple!wmain+53
```

由于 Windows 调试器可以枚举内联函数的所有调用方站点，因此它可以通过计算调用方站点的偏移量来设置内联函数内的断点。 可以使用 [**bm.exe**](bp--bu--bm--set-breakpoint-.md) 命令 (用于设置与正则表达式模式匹配的断点) 为内联函数设置断点。

Windows 调试器将为特定内联函数设置的所有断点组分组到一个断点容器。 你可以 [**使用类似于**](be--breakpoint-enable-.md)、 [**bd**](bd--breakpoint-disable-.md)、 [**bc**](bc--breakpoint-clear-.md)这样的命令来整体处理断点容器。 请参阅以下 **bd 3** 和 **bc 3** 命令示例。 还可以操作各个断点。 请参阅下面的 **2** 个命令示例。

```dbgcmd
0:000> bm simple!MoreCalculate
  2: 00000000`ff6e1455 @!"simple!MoreCalculate" (simple!MoreCalculate inlined in simple!wmain+0x8d)
  4: 00000000`ff6e1528 @!"simple!MoreCalculate" (simple!MoreCalculate inlined in simple!wmain+0x160)

0:000> bl
 0 e 00000000`ff6e13c8 [n:\win7\simple\simple.cpp @ 52]    0001 (0001)  0:**** simple!wmain
 3 e <inline function>     0001 (0001)  0:**** {simple!MoreCalculate}
     2 e 00000000`ff6e1455 [n:\win7\simple\simple.cpp @ 58]    0001 (0001)  0:**** simple!wmain+0x8d (inline function simple!MoreCalculate)
     4 e 00000000`ff6e1528 [n:\win7\simple\simple.cpp @ 72]    0001 (0001)  0:**** simple!wmain+0x160 (inline function simple!MoreCalculate)

0:000> bd 3
0:000> be 2

0:000> bl
 0 e 00000000`ff6e13c8 [n:\win7\simple\simple.cpp @ 52]    0001 (0001)  0:**** simple!wmain
 3 d <inline function>     0001 (0001)  0:**** {simple!MoreCalculate}
     2 e 00000000`ff6e1455 [n:\win7\simple\simple.cpp @ 58]    0001 (0001)  0:**** simple!wmain+0x8d (inline function simple!MoreCalculate)
     4 d 00000000`ff6e1528 [n:\win7\simple\simple.cpp @ 72]    0001 (0001)  0:**** simple!wmain+0x160 (inline function simple!MoreCalculate)

0:000> bc 3

0:000> bl
 0 e 00000000`ff6e13c8 [n:\win7\simple\simple.cpp @ 52]    0001 (0001)  0:**** simple!wmain
```

由于内联函数没有显式调用或返回说明，因此对于调试器而言，源级别单步尤其有挑战性。 例如，如果下一条指令是内联函数) 的一部分，或者可以单步执行和单步跳出同一内联函数，则可能会无意中单步执行内联函数 ( (因为内联函数的代码块已由编译器) 拆分并移动。 为了保持熟悉的单步执行体验，Windows 调试器将为每个代码指令地址维护一个小型概念调用堆栈，并生成一个内部状态计算机来执行单步执行、逐过程执行和跳出操作。 这为非内联函数的单步执行体验提供了合理的近似值。

## <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息


**注意**  可以使用 **inline 0** 命令禁用内联函数调试。 **Inline 1** 命令启用内联函数调试。 [标准调试方法](standard-debugging-techniques.md)

 

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[标准调试方法](standard-debugging-techniques.md)

 

 






