---
title: Bug 检查 0xA3 ACPI_DRIVER_INTERNAL
description: ACPI_DRIVER_INTERNAL bug 检查具有 0x000000A3 值。 此 bug 检查指示 ACPI 驱动程序检测到内部不一致。
ms.assetid: 599c09a9-5c13-404e-b68f-5fa68bd801ed
keywords:
- Bug 检查 0xA3 ACPI_DRIVER_INTERNAL
- ACPI_DRIVER_INTERNAL
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- ACPI_DRIVER_INTERNAL
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 4ab244ec9ef038e9725542420e750a0a1bc3b8a4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544868"
---
# <a name="bug-check-0xa3-acpidriverinternal"></a>Bug 检查 0xA3:ACPI\_DRIVER\_INTERNAL


ACPI\_驱动程序\_内部 bug 检查的值为 0x000000A3。 此 bug 检查指示 ACPI 驱动程序检测到内部不一致。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="acpidriverinternal-parameters"></a>ACPI\_驱动程序\_内部参数


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
<td align="left"><p>保留</p></td>
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

ACPI 驱动程序中的不一致是严重继续运行会导致严重问题。

此问题的一个可能原因是 BIOS 错误。

 

 




