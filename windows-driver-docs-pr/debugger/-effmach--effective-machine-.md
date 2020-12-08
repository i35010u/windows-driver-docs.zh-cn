---
title: .effmach（有效计算机）
description: Effmach 命令显示或更改调试器使用的处理器模式。
keywords:
- 有效的计算机 (. effmach) 命令
- effmach () Windows 调试的有效计算机
ms.date: 01/24/2018
topic_type:
- apiref
api_name:
- .effmach (Effective Machine)
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: c8cb5a7d31664dbb2eb80147d52ce5f823770fb9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817897"
---
# <a name="effmach-effective-machine"></a>.effmach（有效计算机）


**Effmach** 命令显示或更改调试器使用的处理器模式。

```dbgcmd
.effmach [MachineType]
```

## <a name="span-idparametersspanspan-idparametersspanspan-idparametersspanparameters"></a><span id="Parameters"></span><span id="parameters"></span><span id="PARAMETERS"></span>Parameters


<span id="_______MachineType______"></span><span id="_______machinetype______"></span><span id="_______MACHINETYPE______"></span>*MachineType*   
指定调试器用于此会话的处理器类型。 如果省略此参数，则调试器将显示当前计算机类型。

您可以输入以下计算机类型之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>计算机类型</strong></p></td>
<td align="left"><p><strong>说明</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>.</strong></p></td>
<td align="left"><p>使用目标计算机的本机处理器模式的处理器模式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>#</strong></p></td>
<td align="left"><p>对最新事件使用正在执行的代码的处理器模式。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>x86</strong></p></td>
<td align="left"><p>使用基于 x86 的处理器模式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>amd64</strong></p></td>
<td align="left"><p>使用基于 x64 的处理器模式。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>ebc</strong></p></td>
<td align="left"><p>使用 EFI 字节代码处理器模式。</p></td>
</tr>
</tr>
<tr class="odd">
<td align="left"><p><strong>单臂</strong></p></td>
<td align="left"><p>使用 ARM64 处理器模式。</p></td>
</tr>
</tr>
<tr class="evenodd">
<td align="left"><p><strong>chpe</strong></p></td>
<td align="left"><p>使用 CHPE 处理器模式。</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idenvironmentspanspan-idenvironmentspanspan-idenvironmentspanenvironment"></a><span id="Environment"></span><span id="environment"></span><span id="ENVIRONMENT"></span>环境

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>交货</strong></p></td>
<td align="left"><p>用户模式，内核模式</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>目标</strong></p></td>
<td align="left"><p>实时，故障转储</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>平台</strong></p></td>
<td align="left"><p>全部</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

处理器模式影响多种调试器功能：

-   哪个处理器用于堆栈跟踪。

-   进程是使用32位指针还是64位指针。

-   哪个处理器的注册集处于活动状态。

 

 





