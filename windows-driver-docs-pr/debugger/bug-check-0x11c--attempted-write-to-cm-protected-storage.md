---
title: Bug 检查 0x11C ATTEMPTED_WRITE_TO_CM_PROTECTED_STORAGE
description: ATTEMPTED_WRITE_TO_CM_PROTECTED_STORAGE bug 检查的值为0x0000011C，指示已尝试写入到 configuration manager 的受保护存储区。
keywords:
- Bug 检查 0x11C ATTEMPTED_WRITE_TO_CM_PROTECTED_STORAGE
- ATTEMPTED_WRITE_TO_CM_PROTECTED_STORAGE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ATTEMPTED_WRITE_TO_CM_PROTECTED_STORAGE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8bed76289f8e0a2b3f8f62bd529a0c2a3b566b6f
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836899"
---
# <a name="bug-check-0x11c-attempted_write_to_cm_protected_storage"></a>Bug 检查0x11C：尝试 \_ 写入 \_ 到 \_ CM \_ 保护的 \_ 存储


尝试 \_ 写入 \_ \_ CM \_ 受保护的 \_ 存储 Bug 检查的值为0x0000011C。 此 bug 检查指示已尝试写入到 configuration manager 的只读受保护存储区。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="attempted_write_to_cm_protected_storage-parameters"></a>已 \_ 尝试 \_ 写入 \_ CM \_ 保护的 \_ 存储参数


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
<td align="left"><p>尝试写入的虚拟地址</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>PTE 内容</p></td>
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

 

<a name="remarks"></a>备注
-------

如果可能，尝试写入操作的驱动程序的名称将在 "bug 检查" 屏幕上打印为 Unicode 字符串，然后保存到 KiBugCheckDriver 中。

 

 




