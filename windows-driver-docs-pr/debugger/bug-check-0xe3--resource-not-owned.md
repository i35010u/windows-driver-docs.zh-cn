---
title: Bug 检查 0xE3 RESOURCE_NOT_OWNED
description: RESOURCE_NOT_OWNED bug 检查具有 0x000000E3 值。 这表示一个线程尝试释放未拥有的资源。
ms.assetid: f0f47af6-cba0-42a0-912b-562f069d5b3e
keywords:
- Bug 检查 0xE3 RESOURCE_NOT_OWNED
- RESOURCE_NOT_OWNED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- RESOURCE_NOT_OWNED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 7fa5cd04d7c83ec572a7876a9c993fb5b2a85a9f
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67518817"
---
# <a name="bug-check-0xe3-resourcenotowned"></a>Bug 检查 0xE3：资源\_不\_拥有的


资源\_不\_拥有的 bug 检查的值为 0x000000E3。 这表示一个线程尝试释放未拥有的资源。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="resourcenotowned-parameters"></a>资源\_不\_拥有的参数


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
<td align="left"><p>资源的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>线程的地址</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>所有者表 （如果存在） 的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

 

 




