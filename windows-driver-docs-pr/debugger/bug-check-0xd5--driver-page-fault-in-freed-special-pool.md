---
title: Bug 检查 0xD5 DRIVER_PAGE_FAULT_IN_FREED_SPECIAL_POOL
description: DRIVER_PAGE_FAULT_IN_FREED_SPECIAL_POOL bug 检查的值为0x000000D5。 这表明驱动程序已引用先前释放的内存。
ms.assetid: b86e55d2-122f-40ac-adb3-092511d3274e
keywords:
- Bug 检查 0xD5 DRIVER_PAGE_FAULT_IN_FREED_SPECIAL_POOL
- DRIVER_PAGE_FAULT_IN_FREED_SPECIAL_POOL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_PAGE_FAULT_IN_FREED_SPECIAL_POOL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f0f882b4e91ac32d838428b8a81a0fe7d5ada730
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72313784"
---
# <a name="bug-check-0xd5-driver_page_fault_in_freed_special_pool"></a>Bug 检查0xD5：驱动程序\_页面\_错误\_\_释放\_特殊\_池


\_释放的 "驱动程序"\_页面\_错误\_，\_特殊\_池 bug 检查的值为 "0x000000D5"。 这表明驱动程序已引用先前释放的内存。

> [!IMPORTANT]
> 本主题面向程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="driver_page_fault_in_freed_special_pool-parameters"></a>驱动程序\_页面\_错误\_\_释放\_特殊\_池参数


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
<td align="left"><p>引用的内存地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p><strong>0：</strong>读取</p>
<p><strong>1：</strong>写入</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>确定所引用内存的地址（如果已知）</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 
[ **！分析**](https://docs.microsoft.com/windows-hardware/drivers/debugger/-analyze)调试扩展显示有关 bug 检查的信息，可帮助确定根本原因。
如果可以识别负责错误的驱动程序，其名称将打印在蓝色屏幕上，并存储在内存中的位置（PUNICODE\_STRING） **KiBugCheckDriver**。

<a name="cause"></a>原因
-----

"驱动程序验证程序**特殊池**" 选项已发现驱动程序访问先前释放的内存。

有关特殊池的信息，请参阅 Windows 驱动程序工具包的驱动程序验证程序部分。

<a name="remarks"></a>备注
-------

这不能通过**try-except**处理程序来保护--它只能通过探测进行保护。

 

 




