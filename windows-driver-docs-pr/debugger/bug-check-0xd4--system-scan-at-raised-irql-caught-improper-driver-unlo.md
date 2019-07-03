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
ms.openlocfilehash: 755e94d8471b572d9c171596454205af8ff4fade
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67518866"
---
# <a name="bug-check-0xd4-systemscanatraisedirqlcaughtimproperdriverunload"></a>Bug 检查 0xD4：SYSTEM\_SCAN\_AT\_RAISED\_IRQL\_CAUGHT\_IMPROPER\_DRIVER\_UNLOAD


系统\_扫描\_处\_凸起\_IRQL\_CAUGHT\_不恰当\_驱动程序\_卸载 bug 检查的值为 0x000000D4。 这表示，驱动程序未取消挂起操作卸载前倒带。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


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

若要开始调试，请使用内核调试程序获取堆栈跟踪： [ **！ 分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示 bug 检查有关的信息和可有助于确定根本原因，然后使用[**kb （显示堆栈回溯）** ](https://docs.microsoft.com/windows-hardware/drivers/debugger/k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-)命令来获取堆栈跟踪。 如果已确定导致该错误的驱动程序，激活驱动程序验证程序，并尝试复制此 bug。

有关完整详细信息[Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)，请参阅 Windows 驱动程序工具包。

 

 




