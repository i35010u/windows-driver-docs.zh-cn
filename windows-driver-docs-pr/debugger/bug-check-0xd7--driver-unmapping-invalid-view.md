---
title: Bug 检查 0xD7 DRIVER_UNMAPPING_INVALID_VIEW
description: DRIVER_UNMAPPING_INVALID_VIEW bug 检查具有 0x000000D7 值。 这指示一个驱动程序正在尝试取消未映射的地址的映射。
ms.assetid: 68075aa7-f579-49c7-a30a-a21312625ff9
keywords:
- Bug 检查 0xD7 DRIVER_UNMAPPING_INVALID_VIEW
- DRIVER_UNMAPPING_INVALID_VIEW
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_UNMAPPING_INVALID_VIEW
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: db13c60eade91656b43a15d628693533c74a344f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533232"
---
# <a name="bug-check-0xd7-driverunmappinginvalidview"></a>Bug 检查 0xD7:驱动程序\_UNMAPPING\_无效\_视图


该驱动程序\_UNMAPPING\_无效\_视图 bug 检查的值为 0x000000D7。 这指示一个驱动程序正在尝试取消未映射的地址的映射。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="driverunmappinginvalidview-parameters"></a>驱动程序\_UNMAPPING\_无效\_视图参数


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
<td align="left"><p>若要取消映射的虚拟地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p><strong>1:</strong>正在映射视图</p>
<p><strong>2:</strong>正在提交视图</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

可从堆栈跟踪来确定导致该错误的驱动程序。

 

 




