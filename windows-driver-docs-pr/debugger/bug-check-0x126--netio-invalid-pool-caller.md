---
title: Bug 检查 0x126 NETIO_INVALID_POOL_CALLER
description: NETIO_INVALID_POOL_CALLER bug 检查具有 0x00000126 值。 这表示对 netio 托管内存池，例如，前端总线和 MDL 进行了无效的池请求。
ms.assetid: D155D39D-0E8B-4BA5-91B4-AF8F291F7F1F
keywords:
- Bug 检查 0x126 NETIO_INVALID_POOL_CALLER
- NETIO_INVALID_POOL_CALLER
ms.date: 01/30/2019
topic_type:
- apiref
api_name:
- NETIO_INVALID_POOL_CALLER
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4c67d889edbe827b472686d92e5a04a9fcfc7070
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67520743"
---
# <a name="bug-check-0x126-netioinvalidpoolcaller"></a>Bug 检查 0x126：NETIO\_无效\_池\_调用方


NETIO\_无效\_池\_bug 检查调用方的值为 0x00000126。 这表示对 netio 托管内存池，例如，前端总线和 MDL 进行了无效的池请求。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="netioinvalidpoolcaller-parameters"></a>NETIO\_无效\_池\_调用方的参数


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
<td align="left">1</td>
<td align="left"><p>检测的错误子类型。</p>
<p>0x1:无效的池。 池是在无效状态。</p>
参数 2-指向内存块或 MDL。
参数 3 的指向页。
参数 4-指向 CPU 池。
<p>0x2:无效 MDL。 MDL 处于无效状态。</p>
参数 2-MDL 的指针。
参数 3 的指向 CPU 池。
参数 4-指向池标头。</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">请参阅参数 1</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">请参阅参数 1</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">请参阅参数 1</td>
</tr>
</tbody>
</table>

 

 

 




