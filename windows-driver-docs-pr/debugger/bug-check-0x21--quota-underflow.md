---
title: Bug 检查 0x21 QUOTA_UNDERFLOW
description: QUOTA_UNDERFLOW bug 检查的值为0x00000021。 这表明已通过将更多的配额返回给特定的块而不是以前计费的配额，来拆除配额收费。
keywords:
- Bug 检查 0x21 QUOTA_UNDERFLOW
- QUOTA_UNDERFLOW
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- QUOTA_UNDERFLOW
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 9a6e590697c8ac258733a24d2c10c51b2c19df3e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839813"
---
# <a name="bug-check-0x21-quota_underflow"></a>Bug 检查0x21：配额 \_ 下溢


配额 \_ 下溢错误检查的值为0x00000021。 这表明已通过将更多的配额返回给特定的块而不是以前计费的配额，来拆除配额收费。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="quota_underflow-parameters"></a>配额 \_ 下溢参数


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
<td align="left"><p>最初计费的过程（如果有）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>配额类型。 有关所有可能的配额类型值的列表，请参阅 Windows 驱动程序工具包中的标头文件 .Ps (WDK) 。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>要返回的初始计费配额量。</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>未返回的剩余配额量。</p></td>
</tr>
</tbody>
</table>

 

 

 




