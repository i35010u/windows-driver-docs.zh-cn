---
title: Bug 检查 0xC0000218 STATUS_CANNOT_LOAD_REGISTRY_FILE
description: STATUS_CANNOT_LOAD_REGISTRY_FILE bug 检查具有 0xC0000218 值。 这表示无法加载注册表文件。
ms.assetid: cdcf68fa-8beb-4e21-bc6b-7a9f4c6e9e80
keywords:
- Bug 检查 0xC0000218 STATUS_CANNOT_LOAD_REGISTRY_FILE
- STATUS_CANNOT_LOAD_REGISTRY_FILE
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- STATUS_CANNOT_LOAD_REGISTRY_FILE
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 8876d3a3503008aec28ab33006ab3fdc91e5b336
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56544001"
---
# <a name="bug-check-0xc0000218-statuscannotloadregistryfile"></a>Bug 检查 0xC0000218:状态\_无法\_负载\_注册表\_文件


状态\_无法\_负载\_注册表\_文件错误检查的值为 0xC0000218。 这表示无法加载注册表文件。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。

## <a name="statuscannotloadregistryfile-parameters"></a>状态\_无法\_负载\_注册表\_文件参数


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
<td align="left"><p>无法加载的注册表配置单元名称的地址。</p></td>
</tr>
<tr class="even">
<td align="left"><p>2</p></td>
<td align="left"><p>零 （保留）</p></td>
</tr>
<tr class="odd">
<td align="left"><p>3</p></td>
<td align="left"><p>零 （保留）</p></td>
</tr>
<tr class="even">
<td align="left"><p>4</p></td>
<td align="left"><p>零 （保留）</p></td>
</tr>
</tbody>
</table>

 

此 bug 检查显示的说明性文本消息。 损坏的文件的名称显示为消息的一部分。

<a name="cause"></a>原因
-----

无法加载必需的注册表配置单元文件时，将发生此错误。 通常，这意味着文件已损坏或缺失。

在极少数情况下，可以通过一个驱动程序损坏了在内存中，注册表映像，或此区域中的内存错误导致此错误。

<a name="resolution"></a>分辨率
----------

请尝试使用的启动恢复机制 （例如启动修复、 恢复控制台中，或紧急情况下恢复磁盘） 由操作系统提供。 如果问题是缺失或损坏的注册表文件，通常修复问题。

 

 




