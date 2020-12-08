---
title: Bug 检查 0x2A INCONSISTENT_IRP
description: INCONSISTENT_IRP bug 检查的值为0x0000002A。 这表明发现 IRP 包含不一致的信息。
keywords:
- Bug 检查 0x2A INCONSISTENT_IRP
- INCONSISTENT_IRP
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- INCONSISTENT_IRP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 09b384dd22d25f4d1283de7f9373a8eae703cb85
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824691"
---
# <a name="bug-check-0x2a-inconsistent_irp"></a>Bug 检查0x2A： IRP 不一致 \_


不一致的 \_ IRP bug 检查的值为0x0000002A。 这表明发现 IRP 包含不一致的信息。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="inconsistent_irp-parameters"></a>\_IRP 参数不一致


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
<td align="left"><p>发现不一致的 IRP 的地址</p></td>
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

发现 IRP 处于不一致的状态。 通常，这意味着 IRP 的某些字段与 IRP 的剩余状态不一致。 示例是一个已完成的 IRP，但仍标记为排队等候驱动程序的设备队列。

<a name="remarks"></a>备注
-------

此 bug 检查代码当前未在系统中使用，但出于调试目的存在。

 

 




