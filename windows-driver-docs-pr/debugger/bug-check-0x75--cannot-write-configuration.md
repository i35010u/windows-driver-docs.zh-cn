---
title: Bug 检查 0x75 CANNOT_WRITE_CONFIGURATION
description: CANNOT_WRITE_CONFIGURATION bug 检查具有 0x00000075 值。 此 bug 检查指示系统注册表配置单元文件不能转换为映射文件。
ms.assetid: 0190de02-8bd1-4c20-839d-bf9fb517567d
keywords:
- Bug 检查 0x75 CANNOT_WRITE_CONFIGURATION
- CANNOT_WRITE_CONFIGURATION
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- CANNOT_WRITE_CONFIGURATION
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 1f7c51ccf7f02182041c4fac9ad0b3b600978c42
ms.sourcegitcommit: d17b4c61af620694ffa1c70a2dc9d308fd7e5b2e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/22/2019
ms.locfileid: "59902515"
---
# <a name="bug-check-0x75-cannotwriteconfiguration"></a>Bug 检查 0x75：不能\_编写\_配置


无法\_编写\_配置 bug 检查的值为 0x00000075。 此 bug 检查指示系统注册表配置单元文件不能转换为映射文件。

> [!IMPORTANT]
> 本主题面向程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


## <a name="cannotwriteconfiguration-parameters"></a>不能\_编写\_配置参数


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
<td align="left"><p>1</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>导致要假定它具有无法转换该配置单元的 Windows 操作系统 NT 状态代码</p></td>
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

无法\_编写\_如果系统移出池，且 Windows 操作系统不能重新打开该配置单元，通常会出现配置错误检查。

此 bug 检查应几乎永远不会发生，因为 hive 文件的转换，以便足够池应可用于尽可能早地在系统初始化期间发生。

 

 




