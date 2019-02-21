---
title: Bug 检查 0xD4 SYSTEM_SCAN_AT_RAISED_IRQL_CAUGHT_IMPROPER_DRIVER_UNLOAD
description: SYSTEM_SCAN_AT_RAISED_IRQL_CAUGHT_IMPROPER_DRIVER_UNLOAD bug 检查具有 0x000000D4 值。 这表示，驱动程序未取消挂起操作卸载前倒带。
ms.assetid: 4c0e69d1-737c-4dd7-b52a-4cd5eeadcbb9
keywords:
- Bug 检查 0xD4 SYSTEM_SCAN_AT_RAISED_IRQL_CAUGHT_IMPROPER_DRIVER_UNLOAD
- SYSTEM_SCAN_AT_RAISED_IRQL_CAUGHT_IMPROPER_DRIVER_UNLOAD
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SYSTEM_SCAN_AT_RAISED_IRQL_CAUGHT_IMPROPER_DRIVER_UNLOAD
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 87c6fca5c369c86a3aa70a6e47468022c95d8149
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547257"
---
# <a name="bug-check-0xd4-systemscanatraisedirqlcaughtimproperdriverunload"></a>Bug 检查 0xD4:SYSTEM\_SCAN\_AT\_RAISED\_IRQL\_CAUGHT\_IMPROPER\_DRIVER\_UNLOAD


系统\_扫描\_处\_凸起\_IRQL\_CAUGHT\_不恰当\_驱动程序\_卸载 bug 检查的值为 0x000000D4。 这表示，驱动程序未取消挂起操作卸载前倒带。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="systemscanatraisedirqlcaughtimproperdriverunload-parameters"></a>系统\_扫描\_处\_凸起\_IRQL\_CAUGHT\_不恰当\_驱动程序\_卸载参数


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
<p><strong>1:</strong>写入</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>引用内存的地址</p></td>
</tr>
</tbody>
</table>

 

如果无法确定导致错误的驱动程序，其名称是蓝色屏幕上输出和位置在内存中存储 (PUNICODE\_字符串) **KiBugCheckDriver**。

<a name="cause"></a>原因
-----

未能取消后备链列表、 Dpc、 工作线程或其他此类项之前卸载此驱动程序。 随后，系统将尝试访问在引发 IRQL 驱动程序的以前位置。

<a name="resolution"></a>分辨率
----------

若要开始调试，请使用内核调试程序获取堆栈跟踪。 如果已确定导致该错误的驱动程序，激活驱动程序验证程序，并尝试复制此 bug。

有关驱动程序验证程序的完整详细信息，请参阅 Windows 驱动程序工具包。

 

 




