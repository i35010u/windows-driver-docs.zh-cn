---
title: Bug 检查 0xBA SESSION_HAS_VALID_VIEWS_ON_EXIT
description: SESSION_HAS_VALID_VIEWS_ON_EXIT bug 检查具有 0x000000BA 值。 这指示会话驱动程序仍有映射视图时卸载该会话。
ms.assetid: e0ef7d0e-8a3e-41ca-b0c1-c0f0bb298ef1
keywords:
- Bug 检查 0xBA SESSION_HAS_VALID_VIEWS_ON_EXIT
- SESSION_HAS_VALID_VIEWS_ON_EXIT
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- SESSION_HAS_VALID_VIEWS_ON_EXIT
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f29b05f6323b9f5efef6c4b4c87a76ba47887a61
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67519006"
---
# <a name="bug-check-0xba-sessionhasvalidviewsonexit"></a>Bug 检查 0xBA：会话\_HAS\_有效\_视图\_ON\_退出


会话\_HAS\_有效\_视图\_ON\_退出 bug 检查的值为 0x000000BA。 这指示会话驱动程序仍有映射视图时卸载该会话。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="sessionhasvalidviewsonexit-parameters"></a>会话\_HAS\_有效\_视图\_ON\_退出参数


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
<td align="left"><p>会话 ID</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>泄漏的映射视图的数目</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>此会话的地址映射视图表</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>此会话的映射的视图的表的大小</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

不取消映射之前会话卸载其映射的视图的会话驱动程序导致此错误。 这表示 win32k.sys、 atmfd.dll、 rdpdd.dll 或视频驱动程序中的 bug。

 

 




