---
title: irql 扩展命令
description: Irql 扩展显示调试器中断之前对目标计算机上的处理器的中断请求级别 (IRQL)。
ms.assetid: 52dd3b9f-c03c-4b90-a01b-25289de67f5a
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
ms.openlocfilehash: 839226d603c273f23fa76d29c73fea927ea23d57
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56567500"
---
# <a name="irql"></a>!irql


**！ Irql**扩展显示调试器中断之前对目标计算机上的处理器的中断请求级别 (IRQL)。

```dbgcmd
!irql [Processor] 
```

## <a name="span-idddkirqldbgspanspan-idddkirqldbgspanparameters"></a><span id="ddk__irql_dbg"></span><span id="DDK__IRQL_DBG"></span>参数


<span id="_______Processor______"></span><span id="_______processor______"></span><span id="_______PROCESSOR______"></span> *Processor*   
指定的处理器。 输入处理器编号。 如果省略此参数，则调试器将显示当前处理器的 IRQL。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

**！ Irql**扩展选项仅适用于 Windows Server 2003 和更高版本的 Windows。

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

 

### <a name="span-idadditionalinformationspanspan-idadditionalinformationspanspan-idadditionalinformationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>其他信息

于 Irql 有关的信息，请参阅 Windows Driver Kit (WDK) 文档和*Microsoft Windows Internals*由 Mark Russinovich 和 David solomon 合著。 （这些资源可能不可用在某些语言和国家/地区中。）

<a name="remarks"></a>备注
-------

当目标计算机会中断到调试器，IRQL 更改，但保存在调试器中断之前的有效期 IRQL。 **！ Irql**扩展将显示已保存的 IRQL。

同样时出现的 bug 检查和故障转储文件的创建，, 故障转储文件中保存 IRQL 是之前的错误检查，不从该处 IRQL [ **KeBugCheckEx** ](https://msdn.microsoft.com/library/windows/hardware/ff551961)例程执行。

在这两种情况下，当前 IRQL 引发到调度\_级别，除非在 x86 体系结构。 因此，如果发生多个此类事件时，显示 IRQL 也将调度\_级别，使其用处出于调试目的。

[ **！ Pcr** ](-pcr.md)扩展显示当前 IRQL 上所有版本的 Windows，但当前 IRQL 通常不是很有用。 存在的 bug 检查或调试器连接之前，只需 IRQL 更有趣的是，并且这会显示仅与 **！ irql**。

如果提供无效的处理器数目，或已内核损坏，调试器将显示一条消息"无法获得 PRCB 地址"。

下面是输出的来自此扩展插件从双处理器 x86 计算机示例：

```dbgcmd
kd> !irql 0
Debugger saved IRQL for processor 0x0 -- 28 (CLOCK2_LEVEL)

kd> !irql 1
Debugger saved IRQL for processor 0x1 -- 0 (LOW_LEVEL)
```

如果调试器在详细模式中，是包含 IRQL 本身的说明。 下面是从 Itanium 处理器示例：

```dbgcmd
kd> !irql
Debugger saved IRQL for processor 0x0 -- 12 (PC_LEVEL) [Performance counter level]
```

含义 IRQL 数量通常取决于处理器。 下面是一个示例从 x64 处理器。 请注意，IRQL 数与前面的示例中的相同但 IRQL 含义是不同：

```dbgcmd
kd> !irql
Debugger saved IRQL for processor 0x0 -- 12 (SYNCH_LEVEL) [Synchronization level]
```

 

 





