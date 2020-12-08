---
title: Bug 检查 0x12 TRAP_CAUSE_UNKNOWN
description: TRAP_CAUSE_UNKNOWN bug 检查的值为0x00000012。 这表明发生了未知异常。
keywords:
- Bug 检查 0x12 TRAP_CAUSE_UNKNOWN
- TRAP_CAUSE_UNKNOWN
ms.date: 06/26/2018
topic_type:
- apiref
api_name:
- TRAP_CAUSE_UNKNOWN
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 39e7099f2c0d57458dcd975ebd7b2a085994131f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96808501"
---
# <a name="bug-check-0x12-trap_cause_unknown"></a>Bug 检查0x12：陷阱 \_ 原因 \_ 未知


"陷阱 \_ 原因 \_ 未知 bug 检查" 的值为 "0x00000012"。 这表明发生了未知异常。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="trap_cause_unknown-parameters"></a>陷阱 \_ 导致 \_ 未知参数


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">参数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>TRAP_CAUSE_UNKNOWN 的类型</p>
<p><B>VALUES</B></p>
<p>1-意外中断。  (参数2–中断矢量) </p>
<p>2-未知的浮点异常。 </p>
<p>3-启用和断言状态位 (参阅处理器定义) 。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>依赖于 Arg1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>预留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>预留</p></td>
</tr>
</tbody>
</table>

<a name="resolution"></a>解决方法
----------

[**！分析**](-analyze.md)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。

若要开始，请使用 [**k、kb、glm-kc-qnw、kd、kp、kp、kv (显示 Stack Backtrace)**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md) 命令来查看堆栈跟踪。 可以指定处理器编号来检查所有处理器上的堆栈。 

你还可以在代码中设置一个断点，使其导致此 stop 代码，并尝试单步执行出错的代码。

[！ Idt](-idt.md)扩展可用于显示指定中断调度表 (isr) 的中断服务例程 (idt) 。 

[调试中断风暴](debugging-an-interrupt-storm.md)中所述的某些方法可用于意外中断。

有关使用故障转储的常规信息，请参阅 [使用 Windows 调试器进行故障转储分析 (WinDbg) ](crash-dump-files.md)。

如果你不具备使用 Windows 调试器来处理此问题，则可以使用一些基本的故障排除技术。

-   查看事件查看器中的系统日志，以获取可能有助于识别导致此错误检查的设备或驱动程序的其他错误消息。

-   如果驱动程序标识在错误检查消息中，禁用该驱动程序或咨询驱动程序更新的制造商。

-   确认安装的任何新硬件都与安装的 Windows 版本兼容。 例如，可以在 [Windows 10 规范](https://www.microsoft.com/windows/windows-10-specifications)中获取有关所需硬件的信息。

-   有关其他常规疑难解答信息，请参阅 [**蓝屏数据**](blue-screen-data.md)。

 

 

 




