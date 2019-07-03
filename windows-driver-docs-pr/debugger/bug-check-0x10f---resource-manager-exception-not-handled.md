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
ms.openlocfilehash: 3a853937f655a87909e7780bc9f5334bc1d8cca3
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67521334"
---
# <a name="bug-check-0x10f-resourcemanagerexceptionnothandled"></a>Bug 检查 0x10F：资源\_管理器\_异常\_不\_已处理


资源\_管理器\_异常\_不\_已处理错误检查的值为 0x0000010F。 这表示内核事务管理器检测到内核模式资源管理器已引发异常以响应直接调用的回调。 资源管理器是处于意外且不可恢复的状态。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


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

 

 

 




