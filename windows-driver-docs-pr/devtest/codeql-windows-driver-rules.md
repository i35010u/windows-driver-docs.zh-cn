---
title: Windows 驱动程序的 CodeQL 查询
description: 驱动程序的 CodeQL 查询
ms.date: 01/11/2021
ms.localizationpriority: medium
ms.openlocfilehash: bdec8e7265e4d7ab8dee146a5ea11a16e54be0bc
ms.sourcegitcommit: 20569e032b1e0963ad295e9c46b7682832af3d44
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/18/2021
ms.locfileid: "100648132"
---
# <a name="supplemental-windows-driver-codeql-queries"></a>补充的 Windows 驱动程序 CodeQL 查询

本部分列出并描述了一些 [CodeQL 查询](./static-tools-and-codeql.md) ，这些查询是 [Microsoft GitHub CodeQL 存储库](https://github.com/microsoft/Windows-Driver-Developer-Supplemental-Tools) 的一部分，特定于 Windows 平台的驱动程序开发。

## <a name="list-of-queries"></a>查询列表

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">查询名称</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="codeql-windows-driver-wdkdeprecatedapi.md" data-raw-source="[WDK Deprecated API](codeql-windows-driver-wdkdeprecatedapi.md)">WDK 弃用的 API</a></p></td>
<td align="left"><p>查找弃用的池分配 Api 的所有实例</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="codeql-windows-driver-useafterfree.md" data-raw-source="[UseAfterFree](codeql-windows-driver-useafterfree.md)">UseAfterFree</a></p></td>
<td align="left"><p>在 (高精度) 中查找驱动程序源代码中的 UseAfterFree 缺陷的选择实例</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="codeql-windows-driver-probableuseafterfree.md" data-raw-source="[Probable UseAfterFree](codeql-windows-driver-probableuseafterfree.md)">可能的 UseAfterFree</a></p></td>
<td align="left"><p>在 (低精度) 的驱动程序源代码中查找几乎所有 UseAfterFree 缺陷实例</p></td>
</tr>
</tbody>
</table>

 

 

