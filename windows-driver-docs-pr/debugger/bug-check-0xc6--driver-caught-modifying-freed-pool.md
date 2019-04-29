---
title: Bug 检查为 0xC6 DRIVER_CAUGHT_MODIFYING_FREED_POOL
description: DRIVER_CAUGHT_MODIFYING_FREED_POOL bug 检查具有 0x000000C6 值。 这表示该驱动程序试图访问已释放的内存池。
ms.assetid: a5df3612-549d-4cf1-b3e1-4e5efad8ce88
keywords:
- Bug 检查为 0xC6 DRIVER_CAUGHT_MODIFYING_FREED_POOL
- DRIVER_CAUGHT_MODIFYING_FREED_POOL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DRIVER_CAUGHT_MODIFYING_FREED_POOL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ba18a6c3d20937abf6c64160285b63b9323283a6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324677"
---
# <a name="bug-check-0xc6-drivercaughtmodifyingfreedpool"></a>Bug 检查 0xC6：驱动程序\_CAUGHT\_修改\_FREED\_池


该驱动程序\_CAUGHT\_修改\_FREED\_池 bug 检查的值为 0x000000C6。 这表示该驱动程序试图访问已释放的内存池。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="drivercaughtmodifyingfreedpool-parameters"></a>驱动程序\_CAUGHT\_修改\_FREED\_池参数


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
<td align="left"><p><strong>0:</strong>Read</p>
<p><strong>1:</strong>写入</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p><strong>0:</strong>内核模式</p>
<p><strong>1:</strong>用户模式</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

有故障组件将显示在当前内核堆栈。 此驱动程序应替换或调试。

 

 




