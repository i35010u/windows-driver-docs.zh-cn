---
title: Bug 检查 0x36 DEVICE_REFERENCE_COUNT_NOT_ZERO
description: DEVICE_REFERENCE_COUNT_NOT_ZERO bug 检查具有 0x00000036 值。 这表示一个驱动程序尝试删除仍具有积极的引用计数的设备对象。
ms.assetid: 8379d034-44fd-412a-8a2d-d234d41227ac
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
ms.openlocfilehash: 97206fc8e4bda2b67176005504b7a63dadf778a7
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902851"
---
# <a name="bug-check-0x36-devicereferencecountnotzero"></a>Bug 检查 0x36：设备\_引用\_计数\_不\_零


设备\_引用\_计数\_不\_零错误检查的值为 0x00000036。 这表示一个驱动程序尝试删除仍具有积极的引用计数的设备对象。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="devicereferencecountnotzero-parameters"></a>设备\_引用\_计数\_不\_零个参数


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
<td align="left"><p>保留</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>保留</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>保留</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

设备驱动程序已尝试删除的一个设备对象从系统中，但该对象的引用计数为非零。

这意味着没有到设备仍未完成的引用。 （引用计数指示多个原因无法删除此设备对象的原因。）

这是调用的设备驱动程序中的 bug。

 

 




