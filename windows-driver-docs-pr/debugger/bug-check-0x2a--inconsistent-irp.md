---
title: Bug 检查 0x2A INCONSISTENT_IRP
description: INCONSISTENT_IRP bug 检查具有 0x0000002A 值。 这指示 IRP 找来包含不一致的信息。
ms.assetid: e8dcfba1-94ed-499c-ae00-e0dfaf7f5094
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
ms.openlocfilehash: e89eab20adf0ed2b03f4202a3127f46cf5cbb5ae
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544130"
---
# <a name="bug-check-0x2a-inconsistentirp"></a>Bug 检查 0x2A:不一致\_IRP


不一致\_IRP bug 检查的值为 0x0000002A。 这指示 IRP 找来包含不一致的信息。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="inconsistentirp-parameters"></a>不一致\_IRP 参数


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
<td align="left"><p>已发现不一致的 IRP 的地址</p></td>
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

发现 IRP 处于不一致的状态。 通常这意味着 IRP 的某些字段是与 IRP 的剩余状态不一致。 示例将 IRP 的已完成，但仍被标记为正在排队到驱动程序的设备队列。

<a name="remarks"></a>备注
-------

此错误检查代码不当前正在使用在系统中，但用于调试目的。

 

 




