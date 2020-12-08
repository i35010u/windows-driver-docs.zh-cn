---
title: Bug 检查 0x106 AGP_ILLEGALLY_REPROGRAMMED
description: AGP_ILLEGALLY_REPROGRAMMED bug 检查的值为0x00000106。 这表明 (AGP) 硬件的加速图形端口已被未经授权的代理 reprogrammed。
keywords:
- Bug 检查 0x106 AGP_ILLEGALLY_REPROGRAMMED
- AGP_ILLEGALLY_REPROGRAMMED
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- AGP_ILLEGALLY_REPROGRAMMED
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: befae4d1ab334bfd828406562bf97c4ca215172c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96790077"
---
# <a name="bug-check-0x106-agp_illegally_reprogrammed"></a>Bug 检查0x106： AGP \_ 非法 \_ REPROGRAMMED


AGP \_ 非法 \_ REPROGRAMMED bug 检查的值为0x00000106。 这表明 (AGP) 硬件的加速图形端口已被未经授权的代理 reprogrammed。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="agp_illegally_reprogrammed-parameters"></a>AGP \_ 非法 \_ REPROGRAMMED 参数


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
<td align="left"><p>最初编程的 AGP 命令寄存器值</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>当前命令寄存器值</p></td>
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

此 bug 检查通常是由未签名的或未正确测试的视频驱动程序引起的。

<a name="resolution"></a>解决方法
----------

查看视频制造商的网站中是否有更新的显示驱动程序或使用 VGA 模式。

 

 




