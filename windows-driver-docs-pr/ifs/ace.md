---
title: ACE
description: ACE
ms.assetid: efdf43ae-d4d4-4950-9435-e10bf5b75cf2
keywords:
- 访问控制条目 WDK 文件系统
- ACE WDK 的文件系统
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: c09852728fe16ca66bf2b8aaa4306f602e0d0861
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568420"
---
# <a name="ace"></a>ACE





ACE 是访问控制列表 (ACL) 中的访问控制项 (ACE)。

以下是当前定义的 ACE 类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">特性</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ACCESS_ALLOWED_ACE</p></td>
<td align="left"><p>授予指定权限的用户或组。 此 ACE 存储在任意 ACL (DACL)。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ACCESS_DENIED_ACE</p></td>
<td align="left"><p>拒绝向用户或组指定的权限。 此 ACE 存储在 DACL 中。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SYSTEM_AUDIT_ACE</p></td>
<td align="left"><p>指定哪些类型的访问权限会导致系统级审核。 此 ACE 存储在系统 ACL (SACL) 中。</p></td>
</tr>
</tbody>
</table>

 

第四个 ACE 的结构，系统\_警报\_ACE，当前不支持。

ACL 包含一组 Ace。 ACE 定义对一个对象，用于特定用户或组访问权限，或定义生成系统管理消息或警报的特定用户或组的访问类型。 由安全标识符 (SID) 标识的用户或组。

每个 ACE 开头 ACE\_标头结构。 以下标头的数据的格式而异的标头中指定的 ACE 类型。

此结构必须在 32 位边界上对齐。

要求： ntifs.h （包括 ntifs.h）

## <a name="related-topics"></a>相关主题


[**访问\_允许\_ACE**](https://msdn.microsoft.com/library/windows/hardware/ff538796)

[**访问\_拒绝\_ACE**](https://msdn.microsoft.com/library/windows/hardware/ff538831)

[**ACE\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff538847)

[**ACL**](https://msdn.microsoft.com/library/windows/hardware/ff538866)

[**RtlAddAccessAllowedAce**](https://msdn.microsoft.com/library/windows/hardware/ff552092)

[**RtlGetAce**](https://msdn.microsoft.com/library/windows/hardware/ff552288)

[**SID**](https://msdn.microsoft.com/library/windows/hardware/ff556740)

[**SYSTEM\_ALARM\_ACE**](https://msdn.microsoft.com/library/windows/hardware/ff556769)

[**SYSTEM\_AUDIT\_ACE**](https://msdn.microsoft.com/library/windows/hardware/ff556771)

 

 






