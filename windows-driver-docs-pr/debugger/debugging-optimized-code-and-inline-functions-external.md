---
title: 调试优化的代码和内联函数
description: 对于 Windows 8，调试程序和 Windows 编译器得到了增强，以便你可以调试优化的代码并调试内联函数。
ms.assetid: C7BE6B8E-9CF2-471C-A4F9-931C71CCC0FE
keywords:
- 调试优化的代码
- 调试内联函数
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: eca6217b597f3e3419377c903b48fc7e0c6d9b84
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63350595"
---
# <a name="debugging-optimized-code-and-inline-functions"></a>调试优化的代码和内联函数


对于 Windows 8，调试程序和 Windows 编译器得到了增强，以便你可以调试优化的代码并调试内联函数。 调试器将显示参数和局部变量，而不管它们存储在寄存器或堆栈上。 调试器还显示调用堆栈中的内联函数。 对于内联函数，则调试器会显示本地变量，但不是参数。

当代码获取经过优化时，它进行转换，以更快地运行，并使用较少的内存。 有时函数将删除死代码删除、 代码合并或放置内联的函数的结果。 此外可以删除本地变量和参数。 很多代码优化中删除不需要或不使用; 的本地变量其他优化删除归纳变量在循环中。 公共子表达式消除合并在一起的局部变量。

零售版本的 Windows 进行了优化。 因此如果运行 Windows 的零售版本，是特别有用，调试程序，旨在很好地配合优化的代码。 若要使调试优化代码的有效，两个主要功能是必需的：1） 准确显示本地变量和 2） 显示的调用堆栈上的内联函数。

## <a name="span-idaccuratedisplayoflocalvariablesandparametersspanspan-idaccuratedisplayoflocalvariablesandparametersspanspan-idaccuratedisplayoflocalvariablesandparametersspanaccurate-display-of-local-variables-and-parameters"></a><span id="Accurate_display_of_local_variables_and_parameters"></span><span id="accurate_display_of_local_variables_and_parameters"></span><span id="ACCURATE_DISPLAY_OF_LOCAL_VARIABLES_AND_PARAMETERS"></span>本地变量和参数的准确显示


若要简化的本地变量和参数，编译器准确显示将本地变量和参数的有关的位置信息记录在符号 (PDB) 文件。 这些位置记录跟踪变量的存储位置和这些位置是有效的特定代码范围。 这些记录不仅可以帮助跟踪的变量，但还变量的移动的位置 （在寄存器或堆栈槽中）。 例如，参数可能首先在 RCX 寄存器但是移到堆栈槽以释放 RCX，然后移动到在循环中，很大程度使用时的寄存器 R8，然后移到不同的堆栈槽跳出循环的代码时。 Windows 调试器使用 PDB 文件中的大量位置记录，并使用当前指令指针来选择为本地变量和参数的适当位置记录。

此屏幕截图： Visual Studio 中的局部变量窗口显示中优化的 64 位应用程序的参数和函数的局部变量。 参数和局部变量，我们看到，该函数不是以内联方式。

![局部变量窗口的屏幕截图](images/optimizedcode01.png)

可以使用[ **dv-v** ](dv--display-local-variables-.md)命令来查看参数和本地变量的位置。

![屏幕截图，显示的参数和本地变量的位置](images/optimizedcode02.png)

请注意，局部变量窗口显示的参数正确即使它们存储在寄存器中。

除了使用基元类型跟踪变量，位置记录跟踪数据的本地结构和类的成员。 下面的调试器输出会显示本地结构。

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

以下是有关上述调试器输出某些观测值。

-   本地结构**My1**说明了编译器可以分配给寄存器和非连续堆栈槽本地结构数据成员。
-   命令的输出**dt My2**将不同于命令的输出**dt \_IntSum 0xefa60**。 不能假定本地结构将占用连续内存块的堆栈。 情况下**My2**，则只`sum4`保留在原始堆栈阻止; 其他三个数据成员移动到寄存器。
-   某些数据成员可以具有多个位置。 例如， **My2.sum2**有两个位置： 一个是注册 ECX （这将选择 Windows 调试器），另一个是 0xefa60 + 0x4 （原始堆栈槽）。 此外，这可能对基元类型本地变量和 Windows 调试器施加前置试探法来确定要使用哪个位置。 例如，注册位置始终也能带来堆栈位置。

## <a name="span-iddisplayofinlinefunctionsonthecallstackspanspan-iddisplayofinlinefunctionsonthecallstackspanspan-iddisplayofinlinefunctionsonthecallstackspandisplay-of-inline-functions-on-the-call-stack"></a><span id="Display_of_inline_functions_on_the_call_stack"></span><span id="display_of_inline_functions_on_the_call_stack"></span><span id="DISPLAY_OF_INLINE_FUNCTIONS_ON_THE_CALL_STACK"></span>显示的调用堆栈上的内联函数


在代码优化过程的某些功能放置在行中。 也就是说，函数的正文被直接放置在类似的宏扩展代码。 没有任何函数调用并没有返回给调用方。 为便于显示的内联函数，编译器将数据存储在 PDB 文件，可帮助对内联函数 （即，在属于要串联在一起的被调用方函数的调用方函数中的代码块的序列） 代码块进行解码以及本地变量 （这些代码块中指定了作用域本地变量）。 此数据可帮助调试程序堆栈展开中包含内联函数。

假设编译的应用程序和强制执行一个名为函数`func1`为内联。

```cpp
__forceinline int func1(int p1, int p2, int p3)
{
   int num1 = 0;
   int num2 = 0;
   int num3 = 0;
   ...
}
```

可以使用[ **bm** ](bp--bu--bm--set-breakpoint-.md)命令以处设置断点`func1`。

```dbgcmd
0:000> bm MyApp!func1
  1: 000007f6`8d621088 @!"MyApp!func1" (MyApp!func1 inlined in MyApp!main+0x88)
0:000> g

Breakpoint 1 hit
MyApp!main+0x88:
000007f6`8d621088 488d0d21110000  lea     rcx,[MyApp!`string' (000007f6`8d6221b0)]
```

你创建一个单步执行之后`func1`，可以使用[ **k** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令来查看`func1`调用堆栈上。 可以使用[ **dv** ](dv--display-local-variables-.md)命令来查看有关局部变量`func1`。 请注意，本地变量`num3`显示为不可用。 本地变量可在优化代码的原因有多中不可用。 它可能是该变量不会在优化代码中存在。 它可能是，该变量具有尚未初始化或不再使用该变量。

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

如果您看一下第 1 帧的堆栈跟踪中，您所见的局部变量`main`函数。 请注意两个变量存储在寄存器中。

```dbgcmd
0:000> .frame 1
01 00000000`0050fc90 000007f6`8d6213f3 MyApp!main+0x8f

0:000> dv -v
00000000`0050fd08               c = 0n7
@ebx                            b = 0n13
@esi                            a = 0n6
```

Windows 调试器从 PDB 文件，以查找特定函数放置在其中内联的所有位置的聚合数据。 可以使用[ **x** ](x--examine-symbols-.md)命令以列出的所有调用方站点的内联函数。

```dbgcmd
0:000> x simple!MoreCalculate
00000000`ff6e1455 simple!MoreCalculate =  (inline caller) simple!wmain+8d
00000000`ff6e1528 simple!MoreCalculate =  (inline caller) simple!wmain+160

0:000> x simple!Calculate
00000000`ff6e141b simple!Calculate =  (inline caller) simple!wmain+53
```

由于 Windows 调试器可以枚举内联函数的所有调用方站点，它可以通过计算的偏移量，从调用方站点设置在内联函数断点。 可以使用[ **bm** ](bp--bu--bm--set-breakpoint-.md)命令 （这用于设置与正则表达式模式匹配的断点） 若要设置断点的内联函数。

Windows 调试器分组到断点容器设置为特定的内联函数的所有断点。 您可以通过使用类似的命令断点容器操作作为一个整体[**进行**](be--breakpoint-enable-.md)， [ **bd**](bd--breakpoint-disable-.md)， [ **bc**](bc--breakpoint-clear-.md)。 请参阅以下**bd 3**并**bc 3**命令示例。 此外可以处理单个断点。 请参阅以下**为 2**命令示例。

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

因为没有任何显式调用或返回说明内联函数，是特别具有挑战性。 调试器单步执行源代码级别。 例如，你可能无意中步骤对内联函数 （如果下一个指令是一个内联函数的一部分），或无法参与并多次跳出相同的内联函数 (因为已拆分的内联函数的代码块和移动由编译器）。 若要保留单步执行的熟悉体验，Windows 调试器维护每个代码指令地址小概念的调用堆栈，并生成的内部状态机执行步进、 逐过程和单步跳出操作。 这样，单步执行体验相当准确的近似的非内联函数。

## <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息


**请注意**  可以使用 **.inline 0**命令，以禁用调试内联函数。 **.Inline 1**命令启用调试内联函数。 [标准调试技术](standard-debugging-techniques.md)

 

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[标准调试技术](standard-debugging-techniques.md)

 

 






