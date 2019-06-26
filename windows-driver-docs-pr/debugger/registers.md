---
title: 寄存器
description: 寄存器
ms.assetid: fa334c9f-46c6-4288-95ce-43128fff7f03
keywords:
- 内存访问注册
- 注册
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 103c1fc3e2bb486d469d930ba645f9239b8cbf6b
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366434"
---
# <a name="registers"></a>寄存器


## <span id="ddk_registers_dbx"></span><span id="DDK_REGISTERS_DBX"></span>


[调试器引擎](introduction.md#debugger-engine)可以用于检查和更改目标的寄存器。

可在目标上的寄存器取决于其处理器体系结构。 用于 x86 和 Itanium 处理器的寄存器的说明，请参阅[处理器体系结构](processor-architecture.md)。 适用于处理器寄存器的完整说明，请参阅该处理器的文档。

### <a name="span-idtheregistersetspanspan-idtheregistersetspanthe-register-set"></a><span id="the_register_set"></span><span id="THE_REGISTER_SET"></span>注册组

[ **GetNumberRegisters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getnumberregisters)方法可用于在目标上找到的寄存器的数量。

每个注册是通过其索引引用。 第一个寄存器的索引为 0，，最后一个寄存器的索引为的减一的寄存器的数量。 若要查找其名称已知的寄存器的索引，请使用[ **GetIndexByName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getindexbyname)。

该方法[ **GetDescription** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getdescription)返回有关注册的信息。 这包括注册的名称，它可以保存的值的类型以及它是否 subregister。

一个*subregister*包含在另一个寄存器是寄存器。 当 subregister 更改包含它的寄存器也会更改。 例如，在 x86 处理器， **ax** subregister 等同于 32 位的低 16 位**eax**注册。

有三个特殊寄存器，可能会使用以下方法找到的值。 这些寄存器的值的解释取决于依赖于平台。

-   当前指令的位置可能会找到[ **GetInstructionOffset** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getinstructionoffset)并[ **GetInstructionOffset2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getinstructionoffset2)。

-   可能与找到的位置的当前处理器堆栈槽[ **GetStackOffset** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getstackoffset)并[ **GetStackOffset2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getstackoffset2)。

-   对于当前函数的堆栈帧的位置可能会找到[ **GetFrameOffset** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getframeoffset)并[ **GetFrameOffset2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getframeoffset2)。

### <a name="span-idmanipulatingregistersspanspan-idmanipulatingregistersspanmanipulating-registers"></a><span id="manipulating_registers"></span><span id="MANIPULATING_REGISTERS"></span>操作寄存器

可以通过使用该方法读取寄存器的值[ **GetValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getvalue)。 可以通过使用读取多个寄存器[ **GetValues** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getvalues)并[ **GetValues2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getvalues2)。

一个值，可以通过使用方法写入到寄存器[ **SetValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-setvalue)。 可以通过使用编写多个寄存器[ **SetValues** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-setvalues)并[ **SetValues2**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-setvalues2)。

当写入到注册的值，如果提供的值具有不同的类型为寄存器则将值的类型将转换为注册的类型。 此转换是执行该方法的相同[ **CoerceValue**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugcontrol3-coercevalue)。 如果注册的类型不是能够容纳提供的值，此转换可能会导致数据丢失。

### <a name="span-idpseudoregistersspanspan-idpseudoregistersspan-pseudo-registers"></a><span id="pseudo_registers"></span><span id="PSEUDO_REGISTERS"></span> 伪寄存器

*伪寄存器*是由调试器引擎维护的变量，例如，保存某些值， **$teb**是伪寄存器，其值为当前线程的线程环境的地址的名称块 (TEB)。 有关详细信息和伪寄存器列表，请参阅[伪寄存器语法](pseudo-register-syntax.md)。

每个伪寄存器的索引。 索引是一个介于零和伪寄存器的数量 (由[ **GetNumberPseudoRegisters**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getnumberpseudoregisters)) 减一。 若要按名称查找伪寄存器的索引，请使用[ **GetPseudoIndexByName**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getpseudoindexbyname)。 可以使用读取的伪寄存器的值[ **GetPseudoValues**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getpseudovalues)，并且可以将值写入使用伪寄存器[ **SetPseudoValues** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-setpseudovalues). 伪寄存器，包括其类型的说明使用[ **GetPseudoDescription**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-getpseudodescription)。

**请注意**  并非所有伪寄存器都可用的在所有调试会话中或在特定会话中的所有时间。

 

### <a name="span-iddisplayingregistersspanspan-iddisplayingregistersspandisplaying-registers"></a><span id="displaying_registers"></span><span id="DISPLAYING_REGISTERS"></span>显示寄存器

方法[ **OutputRegisters** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-outputregisters)并[ **OutputRegisters2** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugregisters2-outputregisters2)格式目标注册，并将其作为输出发送到客户端。

### <a name="span-ideventsspanspan-ideventsspanevents"></a><span id="events"></span><span id="EVENTS"></span>事件

每当的目标的寄存器的值更改时，引擎将调用[ **IDebugEventCallbacks::ChangeDebuggeeState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugeventcallbacks-changedebuggeestate)带有参数的回调方法*标志*设置为调试\_CDS\_注册。

 

 





