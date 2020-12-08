---
title: Bug 检查 0xA3 ACPI_DRIVER_INTERNAL
description: ACPI_DRIVER_INTERNAL bug 检查的值为0x000000A3。 此错误检查表示 ACPI 驱动程序检测到内部不一致。
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
ms.openlocfilehash: 1e25a95bd82c707f21067ae81abef11fd9bd1237
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819241"
---
# <a name="bug-check-0xa3-acpi_driver_internal"></a>Bug 检查0xA3： ACPI \_ 驱动程序 \_ 内部


ACPI \_ 驱动程序 \_ 内部 bug 检查的值为0x000000A3。 此错误检查表示 ACPI 驱动程序检测到内部不一致。

> [!IMPORTANT]
> 本主题面向程序员。 如果您是在使用计算机时收到蓝屏错误代码的客户，请参阅[蓝屏错误疑难解答](https://www.windows.com/stopcode)。


## <a name="acpi_driver_internal-parameters"></a>ACPI \_ 驱动程序 \_ 内部参数


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

ACPI 驱动程序中的不一致很严重，继续运行会导致严重问题。

此问题的一个可能原因是 BIOS 错误。

 

 




