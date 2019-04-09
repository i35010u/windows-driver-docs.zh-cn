---
title: Bug 检查 0xD5 DRIVER_PAGE_FAULT_IN_FREED_SPECIAL_POOL
description: DRIVER_PAGE_FAULT_IN_FREED_SPECIAL_POOL bug 检查具有 0x000000D5 值。 这指示一个驱动程序具有引用先前释放的内存。
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
ms.openlocfilehash: b8a939289ca411adaa3e5ca6a7a06be1b669c256
ms.sourcegitcommit: 55d7f63bb9e7668d65aa0999e65d18fabd44758e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2019
ms.locfileid: "59238423"
---
# <a name="bug-check-0xd5-driverpagefaultinfreedspecialpool"></a>Bug 检查 0xD5：驱动程序\_页上\_容错\_IN\_FREED\_特殊\_池


该驱动程序\_页上\_容错\_IN\_FREED\_特殊\_池 bug 检查的值为 0x000000D5。 这指示一个驱动程序具有引用先前释放的内存。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="driverpagefaultinfreedspecialpool-parameters"></a>驱动程序\_页上\_容错\_IN\_FREED\_特殊\_池参数


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

 

如果无法确定导致错误的驱动程序，其名称是蓝色屏幕上输出和位置在内存中存储 (PUNICODE\_字符串) **KiBugCheckDriver**。

<a name="cause"></a>原因
-----

Driver Verifier**特殊池**选项捕获访问之前释放的内存的驱动程序。

有关特殊的池的信息，请查阅 Windows 驱动程序工具包的驱动程序验证程序部分。

<a name="remarks"></a>备注
-------

这不会受到**试用-除**处理程序-通过探测来仅进行保护。

 

 




