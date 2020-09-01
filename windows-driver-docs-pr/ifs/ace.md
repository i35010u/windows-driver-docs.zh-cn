---
title: ACE
description: ACE
ms.assetid: efdf43ae-d4d4-4950-9435-e10bf5b75cf2
keywords:
- 访问控制入口 WDK 文件系统
- ACE WDK 文件系统
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1ac0a605808e07a4c20fa941484182c448e05cc1
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066226"
---
# <a name="ace"></a>ACE





ACE 是访问控制列表中 (ACE) 的访问控制项 (ACL) 。

下面是当前定义的 ACE 类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Attribute</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ACCESS_ALLOWED_ACE</p></td>
<td align="left"><p>向用户或组授予指定的权限。 此 ACE 存储在 (DACL) 的任意 ACL 中。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ACCESS_DENIED_ACE</p></td>
<td align="left"><p>拒绝用户或组指定的权限。 此 ACE 存储在 DACL 中。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SYSTEM_AUDIT_ACE</p></td>
<td align="left"><p>指定将导致系统级审核的访问类型。 此 ACE (SACL) 存储在系统 ACL 中。</p></td>
</tr>
</tbody>
</table>

 

当前不支持第四个 ACE 结构， \_ 即系统警报 \_ ACE。

ACL 包含 Ace 的列表。 ACE 定义对特定用户或组的对象的访问，或定义为特定用户或组生成系统管理消息或警报的访问类型。 用户或组由 (SID) 的安全标识符标识。

每个 ACE 都以 ACE \_ 标头结构开始。 标头后面的数据格式因标头中指定的 ACE 类型的不同而异。

此结构必须在32位边界上对齐。

要求： ntifs (包含 ntifs) 

## <a name="related-topics"></a>相关主题


[**访问 \_ 允许的 \_ ACE**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_access_allowed_ace)

[**\_拒绝访问 \_ ACE**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_access_denied_ace)

[**ACE \_ 标头**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_ace_header)

[**ACL**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_acl)

[**RtlAddAccessAllowedAce**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-rtladdaccessallowedace)

[**RtlGetAce**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-rtlgetace)

[**SID**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_sid)

[**系统 \_ 警报 \_ ACE**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_system_alarm_ace)

[**系统 \_ 审核 \_ ACE**](/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_system_audit_ace)

 

