---
title: Bug 检查 0xD6 DRIVER_PAGE_FAULT_BEYOND_END_OF_ALLOCATION
description: DRIVER_PAGE_FAULT_BEYOND_END_OF_ALLOCATION bug 检查的值为0x000000D6。 这表明驱动程序访问的内存超出了其池分配的结尾。
ms.assetid: 939165dc-3052-4de7-88fd-25d4a7e82945
keywords:
- Bug 检查 0xD6 DRIVER_PAGE_FAULT_BEYOND_END_OF_ALLOCATION
- DRIVER_PAGE_FAULT_BEYOND_END_OF_ALLOCATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_PAGE_FAULT_BEYOND_END_OF_ALLOCATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4c72e875365c5b04548a0c0baf3598a596581955
ms.sourcegitcommit: f017184b00f59b088df87a5bd85fec51b7aed8b2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/15/2019
ms.locfileid: "72313782"
---
# <a name="bug-check-0xd6-driver_page_fault_beyond_end_of_allocation"></a>Bug 检查0xD6：驱动\_页面\_错误\_超过\_分配\_结束\_


\_分配 bug 检查\_\_的 "驱动程序" 页错误\_超过\_结束\_的值为 "0x000000D6"。 这表明驱动程序访问的内存超出了其池分配的结尾。

> [!IMPORTANT]
> 本主题面向程序员。 如果你是在使用计算机时收到蓝屏错误代码的客户，请参阅[排查蓝屏错误](https://www.windows.com/stopcode)。


## <a name="driver_page_fault_beyond_end_of_allocation-parameters"></a>驱动\_页面\_错误\_超过\_分配参数\_结束\_


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
如果可以识别负责错误的驱动程序，其名称将打印在蓝色屏幕上，并存储在内存中的位置（PUNICODE\_STRING） *KiBugCheckDriver*。

<a name="cause"></a>原因
-----

驱动程序分配了*n*个字节的内存，然后被引用了超过*n*个字节。 "驱动程序验证器**特殊池**" 选项检测到此冲突。

有关特殊池的信息，请参阅 Windows 驱动程序工具包的驱动程序验证程序部分。

<a name="remarks"></a>备注
-------

这不能通过**try-except**处理程序来保护--它只能通过探测进行保护。

 

 




