---
title: ACE
description: ACE
ms.assetid: efdf43ae-d4d4-4950-9435-e10bf5b75cf2
keywords:
- 访问控制入口 WDK 文件系统
- ACE WDK 文件系统
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4214610341bc78bee0277767d4f6ee4d4fb29060
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841499"
---
# <a name="ace"></a>ACE





ACE 是访问控制列表（ACL）中的访问控制项（ACE）。

下面是当前定义的 ACE 类型。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ACCESS_ALLOWED_ACE</p></td>
<td align="left"><p>向用户或组授予指定的权限。 此 ACE 存储在自由 ACL （DACL）中。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ACCESS_DENIED_ACE</p></td>
<td align="left"><p>拒绝用户或组指定的权限。 此 ACE 存储在 DACL 中。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SYSTEM_AUDIT_ACE</p></td>
<td align="left"><p>指定将导致系统级审核的访问类型。 此 ACE 存储在系统 ACL （SACL）中。</p></td>
</tr>
</tbody>
</table>

 

当前不支持第四个 ACE 结构，系统\_警报\_ACE。

ACL 包含 Ace 的列表。 ACE 定义对特定用户或组的对象的访问，或定义为特定用户或组生成系统管理消息或警报的访问类型。 用户或组由安全标识符（SID）标识。

每个 ACE 都以 ACE\_标头结构开始。 标头后面的数据格式因标头中指定的 ACE 类型的不同而异。

此结构必须在32位边界上对齐。

要求： ntifs （包括 ntifs）

## <a name="related-topics"></a>相关主题


[ **\_ACE 允许访问\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_access_allowed_ace)

[**拒绝访问\_\_ACE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_access_denied_ace)

[**ACE\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_ace_header)

[**ACL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ns-wdm-_acl)

[**RtlAddAccessAllowedAce**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-rtladdaccessallowedace)

[**RtlGetAce**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-rtlgetace)

[**SID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_sid)

[**系统\_警报\_ACE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_system_alarm_ace)

[**系统\_审核\_ACE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/ns-ntifs-_system_audit_ace)

 

 






