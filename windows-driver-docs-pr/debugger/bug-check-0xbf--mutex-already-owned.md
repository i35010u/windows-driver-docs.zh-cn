---
title: Bug 检查 0xBF MUTEX_ALREADY_OWNED
description: MUTEX_ALREADY_OWNED bug 检查的值为0x000000BF。 这表示线程试图获取已拥有的 mutex 的所有权。
keywords:
- Bug 检查 0xBF MUTEX_ALREADY_OWNED
- MUTEX_ALREADY_OWNED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- MUTEX_ALREADY_OWNED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: d7606d55057ce00ea04d6eeb1c3bee1172824a3d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783537"
---
# <a name="bug-check-0xbf-mutex_already_owned"></a>Bug 检查0xBF： \_ 已 \_ 拥有互斥体


\_已拥有的 MUTEX \_ bug 检查的值为0x000000BF。 这表示线程试图获取已拥有的 mutex 的所有权。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="mutex_already_owned-parameters"></a>MUTEX \_ 已经 \_ 拥有参数


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
<td align="left"><p>互斥体的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>导致错误的线程</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>预留</p></td>
</tr>
</tbody>
</table>

 

 

 




