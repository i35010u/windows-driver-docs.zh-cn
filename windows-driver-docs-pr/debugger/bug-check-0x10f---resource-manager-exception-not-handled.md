---
title: Bug 检查 0x10F RESOURCE_MANAGER_EXCEPTION_NOT_HANDLED
description: RESOURCE_MANAGER_EXCEPTION_NOT_HANDLED bug 检查具有 0x0000010F 值。
ms.assetid: d2589163-8c82-4416-a378-a0c72360a9fb
keywords:
- Bug 检查 0x10F RESOURCE_MANAGER_EXCEPTION_NOT_HANDLED
- RESOURCE_MANAGER_EXCEPTION_NOT_HANDLED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- RESOURCE_MANAGER_EXCEPTION_NOT_HANDLED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: ba7d15dda1b695865a23ec3861e039c2e2389754
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525804"
---
# <a name="bug-check-0x10f-resourcemanagerexceptionnothandled"></a>Bug 检查 0x10F:资源\_管理器\_异常\_不\_已处理


资源\_管理器\_异常\_不\_已处理错误检查的值为 0x0000010F。 这表示内核事务管理器检测到内核模式资源管理器已引发异常以响应直接调用的回调。 资源管理器是处于意外且不可恢复的状态。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="resourcemanagerexceptionnothandled-parameters"></a>资源\_管理器\_异常\_不\_HANDLED 参数


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
<td align="left"><p>异常记录的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>上下文记录的地址</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>异常代码的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>资源管理器的地址</p></td>
</tr>
</tbody>
</table>

 

 

 




