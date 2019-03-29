---
title: 汇编和反汇编指令
description: 汇编和反汇编指令
ms.assetid: 7681bea1-4d4e-4260-950d-69cb8feb3807
keywords:
- 调试器引擎 API，组装和拆装功能
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e305e84f3643efb85643d81bd006b432d9ab09fd
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567305"
---
# <a name="assembling-and-disassembling-instructions"></a>汇编和反汇编指令


调试器引擎支持程序集语言的使用，用于显示和更改在目标中的代码。 在调试器中的程序集语言使用的概述，请参阅[在程序集模式下调试](debugging-in-assembly-mode.md)。

**请注意**  所有体系结构不支持程序集语言。 和支持某些体系结构不是所有指令。

 

若要组合的单个程序集语言指令并将生成的处理器指令放在目标计算机的内存中，使用[**组装**](https://msdn.microsoft.com/library/windows/hardware/ff538121)。

若要从目标的处理器指令并生成一个字符串，表示程序集指令反汇编一条指令，请使用[**拆装**](https://msdn.microsoft.com/library/windows/hardware/ff541948)。

该方法[ **GetDisassembleEffectiveOffset** ](https://msdn.microsoft.com/library/windows/hardware/ff546581)返回要拆装的最后一个指令的第一个有效地址。 例如，如果要拆装的最后一个指令`move ax, [ebp+4]`，有效地址为的值`ebp+4`。 这对应于 **$ea**伪寄存器。

若要将已拆装的指令发送到输出回调，使用方法[ *OutputDisassembly* ](https://msdn.microsoft.com/library/windows/hardware/ff553211)并[ *OutputDisassemblyLines* ](https://msdn.microsoft.com/library/windows/hardware/ff553216).

调试器引擎具有控制的程序集和反汇编一些选项。 这些选项返回的[ **GetAssemblyOptions**](https://msdn.microsoft.com/library/windows/hardware/ff545605)。 可以使用设置它们[ **SetAssemblyOptions** ](https://msdn.microsoft.com/library/windows/hardware/ff556626)和一些选项可以与开启[ **AddAssemblyOptions** ](https://msdn.microsoft.com/library/windows/hardware/ff537852)或已关闭与[**RemoveAssemblyOptions**](https://msdn.microsoft.com/library/windows/hardware/ff554483)。

 

 





