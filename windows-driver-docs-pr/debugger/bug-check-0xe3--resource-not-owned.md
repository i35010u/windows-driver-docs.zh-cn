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
ms.openlocfilehash: e3124a079143f07a3b4daebc5fabadc549014802
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63353104"
---
# <a name="bug-check-0xe3-resourcenotowned"></a>Bug 检查 0xE3：资源\_不\_拥有的


资源\_不\_拥有的 bug 检查的值为 0x000000E3。 这表示一个线程尝试释放未拥有的资源。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


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

 

 

 




