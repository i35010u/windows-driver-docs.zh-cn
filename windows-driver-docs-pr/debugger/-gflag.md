---
title: gflag
description: Gflag 扩展插件设置或显示全局标志。
keywords:
- gflag Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- gflag
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e3eaa0c9fc4be7df49d311ad772875005a499110
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824777"
---
# <a name="gflag"></a>!gflag


**！ Gflag** extension 设置或显示全局标志。

```dbgcmd
!gflag [+|-] Value 
!gflag {+|-} Abbreviation 
!gflag -? 
!gflag 
```

## <a name="span-idddk__gflag_dbgspanspan-idddk__gflag_dbgspanparameters"></a><span id="ddk__gflag_dbg"></span><span id="DDK__GFLAG_DBG"></span>参数


<span id="_______Value______"></span><span id="_______value______"></span><span id="_______VALUE______"></span>*值*   
指定32位十六进制数。 如果不使用加号 (**+**) 或减号 (**-**) ，则此数字将成为全局标志位域的新值。 如果在此数字之前添加一个加号 (**+**) ，则该数字将指定一个或多个要设置为1的全局标志位。 如果在此数字之前添加一个减号 (**-**) ，则该数字将指定一个或多个要设置为零的全局标志位。

<span id="_______Abbreviation______"></span><span id="_______abbreviation______"></span><span id="_______ABBREVIATION______"></span>*缩写*   
指定一个全局标志。 *缩写* 是一个由三个字母组成的全局标志的缩写，它设置为 1 (**+**) 或 (**-**) 为零。

<span id="_______-_______"></span> **-?**   
在 [调试器命令窗口](debugger-command-window.md)中显示此扩展的一些帮助文本，包括全局标志缩写的列表。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>Windows 2000</strong></p></td>
<td align="left"><p></p>
Kdextx86.dll Ntsdexts.dll</td>
</tr>
<tr class="even">
<td align="left"><p><strong>Windows XP 及更高版本</strong></p></td>
<td align="left"><p>Exts.dll</p></td>
</tr>
</tbody>
</table>

 

### <a name="span-idadditional_informationspanspan-idadditional_informationspanspan-idadditional_informationspanadditional-information"></a><span id="Additional_Information"></span><span id="additional_information"></span><span id="ADDITIONAL_INFORMATION"></span>附加信息

还可以使用全局标志实用程序 ( # A0) 来设置这些标志。

<a name="remarks"></a>备注
-------

如果未指定任何参数，则 **！ gflag** 扩展将显示当前的全局标志设置。

下表包含可用于 *缩写* 参数的缩写。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">名称</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>0x00000001</p></td>
<td align="left"><p>soe</p></td>
<td align="left"><p>发生异常时停止。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000002</p></td>
<td align="left"><p>购买</p></td>
<td align="left"><p>显示加载程序的快照。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000004</p></td>
<td align="left"><p>.dic</p></td>
<td align="left"><p>Debug 初始命令。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000008</p></td>
<td align="left"><p>"shg"</p></td>
<td align="left"><p>如果 GUI 停止响应，则停止 (即挂起) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000010</p></td>
<td align="left"><p>htc</p></td>
<td align="left"><p>启用堆结尾检查。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000020</p></td>
<td align="left"><p>"hfc"</p></td>
<td align="left"><p>启用堆免费检查。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000040</p></td>
<td align="left"><p>hpc</p></td>
<td align="left"><p>启用堆参数检查。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000080</p></td>
<td align="left"><p>"hvc"</p></td>
<td align="left"><p>在调用时启用堆验证。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000100</p></td>
<td align="left"><p>ptc</p></td>
<td align="left"><p>启用池结尾检查。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000200</p></td>
<td align="left"><p>pfc</p></td>
<td align="left"><p>启用池免费检查。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00000400</p></td>
<td align="left"><p>ptg</p></td>
<td align="left"><p>启用池标记。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00000800</p></td>
<td align="left"><p>"htg"</p></td>
<td align="left"><p>启用堆标记。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00001000</p></td>
<td align="left"><p>ust</p></td>
<td align="left"><p>创建用户模式堆栈跟踪 DB。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00002000</p></td>
<td align="left"><p>"kst"</p></td>
<td align="left"><p>创建内核模式堆栈跟踪 DB。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00004000</p></td>
<td align="left"><p>"otl"</p></td>
<td align="left"><p>维护每种类型的对象的列表。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00008000</p></td>
<td align="left"><p>"htd"</p></td>
<td align="left"><p>启用 DLL 的堆标记。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00010000</p></td>
<td align="left"><p>idp</p></td>
<td align="left"><p>未使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00020000</p></td>
<td align="left"><p>d32</p></td>
<td align="left"><p>启用 Microsoft Win32 子系统的调试。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00040000</p></td>
<td align="left"><p>"ksl"</p></td>
<td align="left"><p>启用内核调试器符号加载。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00080000</p></td>
<td align="left"><p>分发</p></td>
<td align="left"><p>禁用内核堆栈的分页。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00100000</p></td>
<td align="left"><p>"scb"</p></td>
<td align="left"><p>启用关键系统中断。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00200000</p></td>
<td align="left"><p>"dhc"</p></td>
<td align="left"><p>禁用堆合并（免费）。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x00400000</p></td>
<td align="left"><p>ece</p></td>
<td align="left"><p>启用关闭例外。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x00800000</p></td>
<td align="left"><p>"eel"</p></td>
<td align="left"><p>启用异常日志记录。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x01000000</p></td>
<td align="left"><p>eot</p></td>
<td align="left"><p>启用对象句柄类型标记。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x02000000</p></td>
<td align="left"><p>hpa</p></td>
<td align="left"><p>在页面末尾放置堆分配。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x04000000</p></td>
<td align="left"><p>"dwl"</p></td>
<td align="left"><p>调试 WINLOGON。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x08000000</p></td>
<td align="left"><p>ddp</p></td>
<td align="left"><p>禁用内核模式 <strong>DbgPrint</strong> 和 <strong>KdPrint</strong> 输出。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x10000000</p></td>
<td align="left"><p>Null</p></td>
<td align="left"><p>未使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x20000000</p></td>
<td align="left"><p>sue</p></td>
<td align="left"><p>出现未经处理的用户模式异常时停止</p></td>
</tr>
<tr class="odd">
<td align="left"><p>0x40000000</p></td>
<td align="left"><p>Null</p></td>
<td align="left"><p>未使用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>0x80000000</p></td>
<td align="left"><p>dpd</p></td>
<td align="left"><p>禁用受保护的 DLL 验证。</p></td>
</tr>
</tbody>
</table>

 

 

 





