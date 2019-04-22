---
title: Bug 检查 0x12 TRAP_CAUSE_UNKNOWN
description: TRAP_CAUSE_UNKNOWN bug 检查具有 0x00000012 值。 这表示出现了未知的异常。
ms.assetid: 43cbcc34-9df0-4d5f-b823-1cc3cafaa811
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
ms.openlocfilehash: 2262c46d340fc92e602618d00844eb03b43e01d4
ms.sourcegitcommit: fb8b1d2e18dd727e8a479b04c9e6051e7e9fa484
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/18/2019
ms.locfileid: "59239209"
---
# <a name="bug-check-0x12-trapcauseunknown"></a>Bug 检查 0x12：陷阱\_原因\_未知


陷阱\_原因\_未知的错误检查的值为 0x00000012。 这表示出现了未知的异常。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="trapcauseunknown-parameters"></a>陷阱\_原因\_未知的参数


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
<p>1-意外中断。 （参数 2 – 中断矢量）</p>
<p>2-未知浮动点异常。 </p>
<p>3-（请参阅处理器定义） 已启用且断言状态位。</p>
</td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>取决于 Arg1</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

<a name="resolution"></a>分辨率
----------

[ **！ 分析**](-analyze.md)调试扩展显示有关错误检查的信息，有助于在确定根本原因。

若要开始，请检查堆栈跟踪使用[ **k、 kb、 kc、 kd、 kp、 kP，kv （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令。 您可以指定要检查堆栈上的所有处理器的处理器数。 

此外可以导致此停止代码在代码中设置断点并单步前进到出错的代码尝试。

[！ Idt](-idt.md)扩展可用于显示中断服务例程 (Isr) 为指定的中断调度表 (IDT)。 

部分中所述的技术[调试中断的 Storm](debugging-an-interrupt-storm.md)可与意外中断。

有关使用故障转储的常规信息，请参阅[使用 Windows 调试器 (WinDbg) 的故障转储分析](crash-dump-files.md)。

如果您不准备使用 Windows 调试器处理此问题，可以使用一些基本的故障排除方法。

-   检查事件查看器中的系统日志可能有助于识别设备或驱动程序导致此错误检查的其他错误消息。

-   如果驱动程序标识在错误检查消息中，禁用该驱动程序或咨询驱动程序更新的制造商。

-   确认已安装任何新硬件与安装的 Windows 版本兼容。 例如，可以获取有关在所需的硬件信息[Windows 10 规范](https://www.microsoft.com/windows/windows-10-specifications)。

-   有关其他的常规疑难解答信息，请参阅[**蓝色屏幕数据**](blue-screen-data.md)。

 

 

 




