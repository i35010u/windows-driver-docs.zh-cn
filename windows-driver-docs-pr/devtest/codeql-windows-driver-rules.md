---
title: Windows 驱动程序的 CodeQL 查询
description: 驱动程序的 CodeQL 查询
ms.date: 01/11/2021
ms.localizationpriority: medium
ms.openlocfilehash: 6970a45c75beb16a8919e144f2abd8d7fc7a6b6b
ms.sourcegitcommit: 0e165d26ea3887d87eb41d591b8d847038a73085
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/05/2021
ms.locfileid: "106381934"
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
<td align="left"><p>查找弃用的池分配 Api 的实例</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="codeql-windows-driver-useafterfree.md" data-raw-source="[UseAfterFree](codeql-windows-driver-useafterfree.md)">UseAfterFree</a></p></td>
<td align="left"><p>在 (高精度) 中查找驱动程序源代码中的 UseAfterFree 缺陷的选择实例</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="codeql-windows-driver-probableuseafterfree.md" data-raw-source="[Probable UseAfterFree](codeql-windows-driver-probableuseafterfree.md)">可能的 UseAfterFree</a></p></td>
<td align="left"><p>在 (低精度) 的驱动程序源代码中查找几乎所有 UseAfterFree 缺陷实例</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="codeql-windows-driver-padding-byte-information-disclosure.md" data-raw-source="[PaddingByteInformationDisclosure](codeql-windows-driver-padding-byte-information-disclosure.md)">PaddingByteInformationDisclosure</a></p></td>
<td align="left"><p>检查是否有新分配的结构或类，这些结构是逐个成员进行初始化的，因为它们在包含填充字节时可能会泄漏信息。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="codeql-windows-driver-badoverflowguard.md" data-raw-source="[BadOverflowGuard](codeql-windows-driver-badoverflowguard.md)">BadOverflowGuard</a></p></td>
<td align="left"><p>通过与加法的某个自变量进行比较来检查是否有溢出。  如果所有参数类型的大小小于4个字节，则将失败。</p></td>
<tr class="even">
<td align="left"><p><a href="codeql-windows-driver-infiniteloop.md" data-raw-source="[InfiniteLoop](codeql-windows-driver-infiniteloop.md)">InfiniteLoop</a></p></td>
<td align="left"><p>查找循环条件中不同宽度的类型之间的比较，这可能导致循环无法终止。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="codeql-windows-driver-uninitializedptrfield.md" data-raw-source="[UninitializedPtrField](codeql-windows-driver-uninitiazliedptrfield.md)">UninitializedPtrField</a></p></td>
<td align="left"><p>查找未在或过程中初始化的指针字段，因为类构造将导致 null 指针取消引用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="codeql-windows-driver-hardcodedivcng.md" data-raw-source="[HardcodedIVCNG](codeql-windows-driver-hardcodedivcng.md)">HardcodedIVCNG</a></p></td>
<td align="left"><p>查找初始化向量的不正确用法。</p></td>
</tr>
</tbody>
</table>

 

 

