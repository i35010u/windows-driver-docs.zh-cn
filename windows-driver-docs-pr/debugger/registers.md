---
title: 寄存器
description: 寄存器
ms.assetid: fa334c9f-46c6-4288-95ce-43128fff7f03
keywords:
- 内存访问，寄存器
- 寄存器
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac946f23eba52a832422b71a69abbac4a2cf1a11
ms.sourcegitcommit: bb3b62a57ba3aea4a0adeefd2d81993367b7b334
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "88148407"
---
# <a name="registers"></a>寄存器


## <span id="ddk_registers_dbx"></span><span id="DDK_REGISTERS_DBX"></span>


[调试器引擎](introduction.md#debugger-engine)可用于检查和更改目标的寄存器。

目标上的可用寄存器取决于其处理器的体系结构。 有关 x86 处理器寄存器的说明，请参阅[处理器体系结构](processor-architecture.md)。 有关适用于处理器的注册的完整说明，请参阅该处理器的文档。

### <a name="span-idthe_register_setspanspan-idthe_register_setspanthe-register-set"></a><span id="the_register_set"></span><span id="THE_REGISTER_SET"></span>注册集

[**GetNumberRegisters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getnumberregisters)方法可用于查找目标上寄存器的数目。

每个寄存器都按其索引引用。 第一个寄存器的索引为零，最后一个寄存器的索引为寄存器的数目减一。 若要查找名称已知的寄存器的索引，请使用[**GetIndexByName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getindexbyname)。

方法[**GetDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getdescription)返回有关寄存器的信息。 这包括寄存器的名称、它可以包含的值的类型以及它是否为 subregister。

*Subregister*是包含在另一个寄存器中的寄存器。 当 subregister 更改时，包含它的寄存器还会更改。 例如，在 x86 处理器上， **ax** subregister 与32位**eax**寄存器的低16位相同。

有三个特殊寄存器，可以通过使用以下方法找到其值。 这些寄存器的值的解释取决于平台。

-   可以在[**GetInstructionOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getinstructionoffset)和[**GetInstructionOffset2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getinstructionoffset2)中找到当前指令的位置。

-   可以在[**GetStackOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getstackoffset)和[**GetStackOffset2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getstackoffset2)中找到当前处理器堆栈槽的位置。

-   可以在[**GetFrameOffset**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getframeoffset)和[**GetFrameOffset2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getframeoffset2)中找到当前函数的堆栈帧的位置。

### <a name="span-idmanipulating_registersspanspan-idmanipulating_registersspanmanipulating-registers"></a><span id="manipulating_registers"></span><span id="MANIPULATING_REGISTERS"></span>操作寄存器

可以使用方法[**GetValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getvalue)读取寄存器的值。 使用[**GetValues**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getvalues)和[**GetValues2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getvalues2)可以读取多个寄存器。

可以通过使用方法[**SetValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-setvalue)将值写入寄存器。 可以通过使用[**SetValues**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-setvalues)和[**SetValues2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-setvalues2)来编写多个寄存器。

向寄存器写入值时，如果提供的值与寄存器的类型具有不同的类型，则该值将转换为寄存器的类型。 此转换与方法[**CoerceValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugcontrol3-coercevalue)执行的转换相同。 如果寄存器的类型不能容纳提供的值，则此转换可能会导致数据丢失。

### <a name="span-idpseudo_registersspanspan-idpseudo_registersspan-pseudo-registers"></a><span id="pseudo_registers"></span><span id="PSEUDO_REGISTERS"></span>伪寄存器

*伪寄存器*是由调试器引擎维护的变量，用于保存某些值，例如， **$teb**是伪寄存器的名称，其值是当前线程的线程环境块 (teb) 的地址。 有关详细信息和伪寄存器列表，请参阅[伪寄存器语法](pseudo-register-syntax.md)。

每个伪寄存器都有一个索引。 此索引是一个介于零和[**GetNumberPseudoRegisters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getnumberpseudoregisters)) 减1之间返回的伪寄存器 (数之间的数字。 若要按名称查找伪寄存器的索引，请使用[**GetPseudoIndexByName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getpseudoindexbyname)。 使用[**GetPseudoValues**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getpseudovalues)可以读取伪寄存器的值，并且可以使用[**SetPseudoValues**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-setpseudovalues)将值写入伪寄存器。 有关伪寄存器（包括其类型）的说明，请使用[**GetPseudoDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-getpseudodescription)。

**注意**   并非所有的伪寄存器在所有调试会话中都可用，也不会在特定会话中出现。

 

### <a name="span-iddisplaying_registersspanspan-iddisplaying_registersspandisplaying-registers"></a><span id="displaying_registers"></span><span id="DISPLAYING_REGISTERS"></span>显示寄存器

[**OutputRegisters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-outputregisters)和[**OutputRegisters2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugregisters2-outputregisters2)方法用于格式化目标的寄存器，并将其作为输出发送到客户端。

### <a name="span-ideventsspanspan-ideventsspanevents"></a><span id="events"></span><span id="EVENTS"></span>事件

每当目标的寄存器值发生更改时，引擎将调用[**IDebugEventCallbacks：： ChangeDebuggeeState**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugeventcallbacks-changedebuggeestate)回调方法，并将参数*标志*设置为 "调试 \_ cd 寄存器" \_ 。

 

 





