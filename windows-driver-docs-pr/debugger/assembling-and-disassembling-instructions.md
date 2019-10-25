---
title: 汇编和反汇编指令
description: 汇编和反汇编指令
ms.assetid: 7681bea1-4d4e-4260-950d-69cb8feb3807
keywords:
- 调试器引擎 API、组装和拆装
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24e64983fdcbb1e1a2b7840a3f78920cdf5c9033
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837640"
---
# <a name="assembling-and-disassembling-instructions"></a>汇编和反汇编指令


调试器引擎支持使用汇编语言来显示和更改目标中的代码。 有关如何在调试器中使用汇编语言的概述，请参阅[在程序集模式下进行调试](debugging-in-assembly-mode.md)。

**请注意**，对于所有体系结构，不支持   汇编语言。 在某些体系结构上，并非所有说明都受支持。

 

若要汇编单个汇编语言指令并将生成的处理器指令放入目标的内存中，请使用 "[**汇编**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-assemble)"。

若要通过从目标获取处理器指令来拆装单个指令，并生成表示程序集指令的字符串，请使用[**反汇编**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-disassemble)。

方法[**GetDisassembleEffectiveOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getdisassembleeffectiveoffset)返回要反汇编的最后一个指令的第一个有效地址。 例如，如果要反汇编的最后一个指令为 `move ax, [ebp+4]`，则有效地址为 `ebp+4`的值。 这对应于 **$ea**伪寄存器。

若要向输出回调发送反汇编说明，请使用[*OutputDisassembly*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-outputdisassembly)和[*OutputDisassemblyLines*](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-outputdisassemblylines)方法。

调试器引擎有一些控制程序集和反汇编的选项。 这些选项由[**GetAssemblyOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-getassemblyoptions)返回。 可以使用[**SetAssemblyOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-setassemblyoptions)设置这些选项，并且可以使用[**AddAssemblyOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-addassemblyoptions)打开某些选项，也可以使用[**RemoveAssemblyOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-removeassemblyoptions)打开。

 

 





