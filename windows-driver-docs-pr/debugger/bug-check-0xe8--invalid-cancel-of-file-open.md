---
title: Bug 检查 0xE8 INVALID_CANCEL_OF_FILE_OPEN
description: INVALID_CANCEL_OF_FILE_OPEN bug 检查具有 0x000000E8 值。 这表示，无效的文件对象传递给 IoCancelFileOpen。
ms.assetid: 168d8b3a-62a0-4436-9e97-812ddfb8b7f7
keywords:
- Bug 检查 0xE8 INVALID_CANCEL_OF_FILE_OPEN
- INVALID_CANCEL_OF_FILE_OPEN
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- INVALID_CANCEL_OF_FILE_OPEN
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 3c584759aea989de4b58d5e13f8e6620f01139a3
ms.sourcegitcommit: d03b44343cd32b3653d0471afcdd3d35cb800c0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2019
ms.locfileid: "67518800"
---
# <a name="bug-check-0xe8-invalidcanceloffileopen"></a>Bug 检查 0xE8：无效\_取消\_OF\_文件\_打开


无效\_取消\_OF\_文件\_打开 bug 检查的值为 0x000000E8。 这表示无效的文件对象传递给**IoCancelFileOpen**。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://www.windows.com/stopcode)。


## <a name="invalidcanceloffileopen-parameters"></a>无效\_取消\_OF\_文件\_打开参数


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
<td align="left"><p>该文件对象传递给<strong>IoCancelFileOpen</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>设备对象传递给<strong>IoCancelFileOpen</strong></p></td>
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

该文件对象传递给**IoCancelFileOpen**无效。 它应该拥有一个引用。 调用的驱动程序**IoCancelFileOpen**出现故障。

 

 




