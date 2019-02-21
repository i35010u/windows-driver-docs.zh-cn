---
title: Bug 检查 0xD1 DRIVER_IRQL_NOT_LESS_OR_EQUAL
description: DRIVER_IRQL_NOT_LESS_OR_EQUAL bug 检查具有 0x000000D1 值。 这表示内核模式驱动程序试图访问可分页内存过高的 IRQL 的进程。
ms.assetid: 26cfd881-cc6e-4cc3-b464-e67d75700b96
keywords:
- Bug 检查 0xD1 DRIVER_IRQL_NOT_LESS_OR_EQUAL
- DRIVER_IRQL_NOT_LESS_OR_EQUAL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_IRQL_NOT_LESS_OR_EQUAL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 394644d10612dec67a93c6da1452ae43cc55c8e5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523053"
---
# <a name="bug-check-0xd1-driverirqlnotlessorequal"></a>Bug 检查 0xD1:DRIVER\_IRQL\_NOT\_LESS\_OR\_EQUAL


该驱动程序\_IRQL\_不\_较少\_或\_相等 bug 检查的值为 0x000000D1。 这表示内核模式驱动程序试图访问可分页内存过高的 IRQL 的进程。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="driverirqlnotlessorequal-parameters"></a>驱动程序\_IRQL\_不\_较少\_或\_等于参数


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
<td align="left"><p>引用的内存</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>在引用的时间的 IRQL</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><strong>0:</strong>Read</p>
<p><strong>1:</strong>写入</p>
<p><strong>8:</strong>执行</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>引用内存的地址</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

驱动程序尝试访问的可分页 （或者是完全无效） 的地址在 IRQL 是否过高。

检查此错误通常被由于驱动程序使用不正确的地址。

如果第一个参数具有相同的值作为第四个参数，并且第三个参数指示执行操作，此 bug 检查可能导致由驱动程序尝试执行代码时代码本身已调出。页面错误的可能原因包括：

-   该函数被标记为可分页，并在提升的 IRQL （其中包括获取锁） 运行。

-   另一个驱动程序中的函数执行函数调用，该驱动程序已被卸载。

-   调用函数时使用了无效的指针的函数指针。

<a name="resolution"></a>分辨率
----------

[ **！ 分析**](-analyze.md)调试扩展显示有关错误检查的信息和确定根本原因非常有帮助。

有关详细信息，请参阅[使用 Windows 调试器 (WinDbg) 的故障转储分析](crash-dump-files.md)

若要开始，请检查堆栈跟踪使用[ **k、 kb、 kc、 kd、 kp、 kP，kv （显示堆栈回溯）** ](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)命令。

如果问题由正在开发的驱动程序，请确保在检查错误时执行的函数的未标记为可分页或不调用任何其他无法换出的内联函数。

如果您不准备使用 Windows 调试器处理此问题，可以使用一些基本的故障排除方法。

-   检查事件查看器中的系统日志可能有助于识别设备或驱动程序导致此错误检查的其他错误消息。

-   如果驱动程序标识在错误检查消息中，禁用该驱动程序或咨询驱动程序更新的制造商。

-   确认已安装任何新硬件与安装的 Windows 版本兼容。 例如，可以获取有关在所需的硬件信息[Windows 10 规范](https://www.microsoft.com/windows/windows-10-specifications)。

-   有关其他的常规疑难解答信息，请参阅[**蓝色屏幕数据**](blue-screen-data.md)。

 

 




