---
title: Bug 检查 0x14A KERNEL_WMI_INTERNAL
description: KERNEL_WMI_INTERNAL bug 检查的值为0x0000014A。 这表明内部内核 WMI 子系统遇到错误。
keywords:
- Bug 检查 0x14A KERNEL_WMI_INTERNAL
- KERNEL_WMI_INTERNAL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- KERNEL_WMI_INTERNAL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: f23a3f864f1c0c7d05c6c98ed08775f3c61b7ec1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840219"
---
# <a name="bug-check-0x14a-kernel_wmi_internal"></a>Bug 检查0x14A：内核 \_ WMI \_ 内部


内核 \_ WMI \_ 内部错误检查的值为0x0000014A。 这表明内部内核 WMI 子系统遇到错误。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="kernel_wmi_internal-parameters"></a>内核 \_ WMI \_ 内部参数


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
<td align="left"><p>0：内核 WMI 条目引用计数已从0递增。</p>
参数2：指向内核 WMI 项的指针。
<p>1：已过早删除内核 WMI 数据源。</p>
参数2：指向内核 WMI 数据源的指针。</td>
</tr>
<tr class="even">
<td align="left">2</td>
<td align="left">请参阅参数1</td>
</tr>
<tr class="odd">
<td align="left">3</td>
<td align="left">预留</td>
</tr>
<tr class="even">
<td align="left">4</td>
<td align="left">预留</td>
</tr>
</tbody>
</table>

 

 

 




