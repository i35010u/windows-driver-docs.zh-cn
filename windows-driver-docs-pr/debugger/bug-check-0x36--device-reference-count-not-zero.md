---
title: Bug 检查 0x36 DEVICE_REFERENCE_COUNT_NOT_ZERO
description: DEVICE_REFERENCE_COUNT_NOT_ZERO bug 检查的值为0x00000036。 这表明驱动程序已尝试删除仍具有肯定引用计数的设备对象。
keywords:
- Bug 检查 0x36 DEVICE_REFERENCE_COUNT_NOT_ZERO
- DEVICE_REFERENCE_COUNT_NOT_ZERO
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- DEVICE_REFERENCE_COUNT_NOT_ZERO
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 17b2220d0b095085796e2d2d1fffacb2d019d066
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837009"
---
# <a name="bug-check-0x36-device_reference_count_not_zero"></a>Bug 检查0x36：设备 \_ 引用 \_ 计数 \_ 不 \_ 为零


设备 \_ 引用 \_ 计数 \_ 不 \_ 为零 bug 检查的值为0x00000036。 这表明驱动程序已尝试删除仍具有肯定引用计数的设备对象。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="device_reference_count_not_zero-parameters"></a>设备 \_ 引用 \_ 计数 \_ 不是 \_ 零参数


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
<td align="left"><p>设备对象的地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>预留</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>预留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>预留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

设备驱动程序已尝试从系统中删除其中一个设备对象，但该对象的引用计数不为零。

这意味着对设备的引用仍未完成。  (引用计数表示无法删除此设备对象的原因数。 ) 

这是调用设备驱动程序中的一个 bug。

 

 




