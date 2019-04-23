---
title: Bug 检查 0xD6 DRIVER_PAGE_FAULT_BEYOND_END_OF_ALLOCATION
description: DRIVER_PAGE_FAULT_BEYOND_END_OF_ALLOCATION bug 检查具有 0x000000D6 值。 这表示其池分配的末尾之外的驱动程序访问内存。
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
ms.openlocfilehash: 38deede965ff4eca12381d2b3f36f8c5a9c61ad4
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59903911"
---
# <a name="bug-check-0xd6-driverpagefaultbeyondendofallocation"></a>Bug 检查 0xD6：驱动程序\_页上\_容错\_超出\_最终\_OF\_分配


驱动程序\_页上\_容错\_超出\_最终\_OF\_分配错误检查的值为 0x000000D6。 这表示其池分配的末尾之外的驱动程序访问内存。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="driverpagefaultbeyondendofallocation-parameters"></a>驱动程序\_页上\_容错\_超出\_最终\_OF\_分配参数


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
<td align="left"><p><strong>0:</strong>Read</p>
<p><strong>1:</strong>写入</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>（如果已知） 引用内存的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

如果无法确定导致错误的驱动程序，其名称是蓝色屏幕上输出和位置在内存中存储 (PUNICODE\_字符串) *KiBugCheckDriver*。

<a name="cause"></a>原因
-----

驱动程序分配*n*字节的内存，然后引用多个*n*字节。 Driver Verifier**特殊池**选项检测到此冲突。

有关特殊的池的信息，请查阅 Windows 驱动程序工具包的驱动程序验证程序部分。

<a name="remarks"></a>备注
-------

这不会受到**试用-除**处理程序-通过探测来仅进行保护。

 

 




