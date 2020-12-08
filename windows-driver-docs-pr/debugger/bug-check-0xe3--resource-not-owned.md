---
title: Bug 检查 0xE3 RESOURCE_NOT_OWNED
description: RESOURCE_NOT_OWNED bug 检查的值为0x000000E3。 这表示线程尝试释放它不拥有的资源。
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
ms.openlocfilehash: 66df5ae7b28baf3cf1461f4b171a2fb3868cae36
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816399"
---
# <a name="bug-check-0xe3-resource_not_owned"></a>Bug 检查0xE3：资源 \_ 未 \_ 拥有


资源 \_ 未 \_ 拥有 bug 检查的值为0x000000E3。 这表示线程尝试释放它不拥有的资源。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="resource_not_owned-parameters"></a>资源 \_ 非 \_ 拥有参数


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
<td align="left"><p>资源地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>线程的地址</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>所有者表 (的地址（如果存在）) </p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>预留</p></td>
</tr>
</tbody>
</table>

 

 

 




