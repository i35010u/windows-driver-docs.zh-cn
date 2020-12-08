---
title: Bug 检查 0x104 AGP_INVALID_ACCESS
description: AGP_INVALID_ACCESS bug 检查的值为0x00000104。 这表明，写入一系列加速图形端口的 GPU (AGP) 内存之前未提交。
keywords:
- Bug 检查 0x104 AGP_INVALID_ACCESS
- AGP_INVALID_ACCESS
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- AGP_INVALID_ACCESS
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2c28d9fcb37b2f239039e659d093d45e55cda67d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96793293"
---
# <a name="bug-check-0x104-agp_invalid_access"></a>Bug 检查0x104： AGP \_ 无效 \_ 访问


AGP \_ 无效 \_ 访问 bug 检查的值为0x00000104。 这表明，写入一系列加速图形端口的 GPU (AGP) 内存之前未提交。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="agp_invalid_access-parameters"></a>AGP \_ 无效 \_ 访问参数


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
<td align="left"><p>将 AGP 验证器页中的 ULONG)  (到已损坏的第一个 ULONG 数据的偏移量</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>0</p></td>
</tr>
</tbody>
</table>

 

<a name="cause"></a>原因
-----

通常，此 bug 检查是由未签名或未正确测试的视频驱动程序引起的。 它也可能由旧的 BIOS 引起。

<a name="resolution"></a>解决方法
----------

检查显示器驱动程序和计算机 BIOS 更新。

 

 




