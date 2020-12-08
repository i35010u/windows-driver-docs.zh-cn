---
title: irql 扩展命令
description: Irql 扩展显示在调试器中断之前目标计算机上的处理器的中断请求级别 (IRQL) 。
keywords:
- IRQL
- 中断请求级别
- irql Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- irql
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8e5de42840def3df5f5ae78a3a158e29649a8a48
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827365"
---
# <a name="irql"></a>!irql


在调试程序中断之前，在目标计算机上的处理器上，% **irql** 扩展显示处理器的中断请求级别 (irql) 。

```dbgcmd
!irql [Processor] 
```

## <a name="span-idddk__irql_dbgspanspan-idddk__irql_dbgspanparameters"></a><span id="ddk__irql_dbg"></span><span id="DDK__IRQL_DBG"></span>参数


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span>*处理器*   
指定处理器。 输入处理器编号。 如果省略此参数，则调试器会显示当前处理器的 IRQL。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

**！ Irql** 扩展仅在 windows Server 2003 和更高版本的 windows 中可用。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP</strong></p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>Windows Server 2003 及更高版本</strong></p></td>
<td align="left"><p>Kdexts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

有关 IRQLs 的信息，请参阅 Windows 驱动程序工具包 (WDK) 文档和 *Microsoft Windows 内部机制* ，Mark Russinovich 和 David 所罗门群岛。

<a name="remarks"></a>备注
-------

当目标计算机中断到调试器时，将更改 IRQL，但在调试器中断之前有效的 IRQL 会被保存。 **！ Irql** 扩展显示保存的 irql。

同样，当发生 bug 检查并创建故障转储文件时，保存在崩溃转储文件中的 IRQL 是在 bug 检查之前立即发生的，而不是执行 [**KeBugCheckEx**](/windows-hardware/drivers/ddi/wdm/nf-wdm-kebugcheckex) 例程时的 irql。

在这两种情况下，当前 IRQL 会引发到调度 \_ 级别，但 x86 体系结构除外。 因此，如果发生多个此类事件，则显示的 IRQL 还会成为调度 \_ 级别，使其在调试时毫无用处。

[**！ Pcr**](-pcr.md)扩展在所有版本的 Windows 上显示当前的 irql，但当前的 irql 通常不起作用。 紧靠 bug 检查或调试器连接之前存在的 IRQL 更有趣，这仅显示为 **！！**。

如果提供了无效的处理器号，或者内核已损坏，则调试器会显示消息 "无法获取 PRCB 地址"。

下面是来自双处理器 x86 计算机的此扩展的输出示例：

```dbgcmd
kd> !irql 0
Debugger saved IRQL for processor 0x0 -- 28 (CLOCK2_LEVEL)

kd> !irql 1
Debugger saved IRQL for processor 0x1 -- 0 (LOW_LEVEL)
```

如果调试器处于详细模式，则包含 IRQL 本身的说明。

IRQL 数字的含义通常取决于处理器。 下面是 x64 处理器的示例。 请注意，IRQL 号码与上一个示例中的相同，但 IRQL 含义不同：

```dbgcmd
kd> !irql
Debugger saved IRQL for processor 0x0 -- 12 (SYNCH_LEVEL) [Synchronization level]
```

 

