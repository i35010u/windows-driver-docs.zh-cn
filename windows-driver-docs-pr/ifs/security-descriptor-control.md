---
title: 安全 \_ 描述符 \_ 控件
description: 安全 \_ 描述符 \_ 控件
ms.assetid: 6a7fe617-156d-4eb0-83f7-df78104acbde
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: baf8cb9256e68cafb59a73c95fed03af1c304dd2
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89067358"
---
# <a name="security_descriptor_control"></a>安全 \_ 描述符 \_ 控件


**安全 \_ 描述符 \_ 控件**类型是一组限制[**安全 \_ 描述符**](/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))结构或其组件含义的位标志。 每个安全描述符都有一个存储**安全 \_ 描述符 \_ 控制**位的**控件**成员。

安全 \_ 描述符 \_ 控件

``` syntax
typedef USHORT SECURITY_DESCRIPTOR_CONTROL, *PSECURITY_DESCRIPTOR_CONTROL;
```

控制值可以包括以下 **安全 \_ 描述符 \_ 控件** 位标志的组合：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">值</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>SE_DACL_AUTO_INHERIT_REQ</p></td>
<td align="left"><p>请求受安全描述符保护的对象的提供程序自动将 DACL 传播到现有子对象。 如果访问接口支持自动继承，则会将 DACL 传播到任何现有子对象，并设置该对象及其子对象的安全说明符中的 SE_DACL_AUTO_INHERITED 位。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_DACL_AUTO_INHERITED</p></td>
<td align="left"><p>从 Windows 2000 开始，表示一个安全描述符，其中 DACL 支持将可继承 Ace 自动传播到现有子对象。</p>
<p>对于支持自动继承的 Windows 2000 Acl，将始终设置此位。 它用于将这些 Acl 与不支持自动继承的 Windows NT 4.0 Acl 区分开来。</p>
<p>此位未在 Windows NT 4.0 及更早版本的安全描述符中设置，后者不支持可继承的 Ace 的自动传播。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SE_DACL_DEFAULTED</p></td>
<td align="left"><p>指示具有默认 DACL 的安全描述符。 例如，如果对象的创建者未指定 DACL，则对象从创建者的访问令牌接收默认的 DACL。 对于 ACE 继承，此标志可能会影响系统对 DACL 的处理方式。 如果未设置 SE_DACL_PRESENT 标志，系统将忽略此标志。</p>
<p>此标志用于确定如何计算对象上的最终 DACL，并使其不会以物理方式存储在安全对象的安全描述符控件中。</p>
<p>若要设置此标志，请使用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlsetdaclsecuritydescriptor" data-raw-source="[&lt;strong&gt;RtlSetDaclSecurityDescriptor&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlsetdaclsecuritydescriptor)"><strong>RtlSetDaclSecurityDescriptor</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_DACL_PRESENT</p></td>
<td align="left"><p>指示具有 DACL 的安全描述符。 如果未设置此标志，或者如果设置了此标志并且 DACL 为 <strong>NULL</strong>，则安全描述符允许所有人都具有完全访问权限。</p>
<p>此标志用于保存由调用方指定的安全信息，直到安全描述符与安全对象关联。 安全描述符与某个安全对象关联后，将始终在安全描述符控件中设置 SE_DACL_PRESENT 标志。</p>
<p>若要设置此标志，请使用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlsetdaclsecuritydescriptor" data-raw-source="[&lt;strong&gt;RtlSetDaclSecurityDescriptor&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlsetdaclsecuritydescriptor)"><strong>RtlSetDaclSecurityDescriptor</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SE_DACL_PROTECTED</p></td>
<td align="left"><p>保护安全描述符的 DACL 不被可继承的 Ace 修改。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_DACL_UNTRUSTED</p></td>
<td align="left"><p>指示由安全描述符的 DACL 指向的 ACL 由不受信任的源提供。 如果设置了此标志并遇到复合 ACE，则系统将在 Ace 中替换服务器 Sid 的已知有效 Sid。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SE_GROUP_DEFAULTED</p></td>
<td align="left"><p>默认机制，而不是安全描述符的原始提供程序（提供安全描述符的组 SID）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_OWNER_DEFAULTED</p></td>
<td align="left"><p>默认机制，而不是安全描述符的原始提供程序（提供安全描述符的所有者安全标识符） (SID) 。 若要设置此标志，请使用 <a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-rtlsetownersecuritydescriptor" data-raw-source="[&lt;strong&gt;RtlSetOwnerSecurityDescriptor&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-rtlsetownersecuritydescriptor)"><strong>RtlSetOwnerSecurityDescriptor</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SE_RM_CONTROL_VALID</p></td>
<td align="left"><p>指示安全描述符中的资源控制管理器位有效。 资源管理器控制位是<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556610(v=vs.85)" data-raw-source="[&lt;strong&gt;SECURITY_DESCRIPTOR&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))"><strong>SECURITY_DESCRIPTOR</strong></a>结构的<strong>Sbz1</strong>成员中的八位，其中包含特定于访问结构的资源管理器的信息。  (有关详细信息，请参阅适用于 Windows 7 的 Microsoft Windows 软件开发工具包 (SDK) 和 .NET Framework 4.0 文档。 ) </p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_SACL_AUTO_INHERIT_REQ</p></td>
<td align="left"><p>请求受安全描述符保护的对象的提供程序自动将 SACL 传播到现有子对象。 如果访问接口支持自动继承，则会将 SACL 传播到任何现有子对象，并设置该对象及其子对象的安全说明符中的 SE_SACL_AUTO_INHERITED 位。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SE_SACL_AUTO_INHERITED</p></td>
<td align="left"><p>指示一个安全描述符，其中 SACL 支持将可继承 Ace 自动传播到现有子对象。 仅当已为对象及其现有子对象执行了自动继承算法时，才设置此位。</p>
<p>此位未在 Windows NT 4.0 及更早版本的安全描述符中设置，后者不支持可继承的 Ace 的自动传播。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_SACL_DEFAULTED</p></td>
<td align="left"><p>默认机制，而不是安全描述符的原始提供程序，前提是 SACL。 对于 ACE 继承，此标志可能会影响系统处理 SACL 的方式。 如果未设置 SE_SACL_PRESENT 标志，系统将忽略此标志。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SE_SACL_PRESENT</p></td>
<td align="left"><p>指示具有 SACL 的安全描述符。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_SACL_PROTECTED</p></td>
<td align="left"><p>保护安全描述符的 SACL 不被可继承的 Ace 修改。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SE_SELF_RELATIVE</p></td>
<td align="left"><p>指示一个自相关格式的安全描述符，其中的所有安全信息在一个连续的内存块中。 如果未设置此标志，则安全描述符为绝对格式。 有关详细信息，请参阅 Windows SDK 文档中的 "绝对和自相关安全描述符"。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_SERVER_SECURITY</p></td>
<td align="left"><p>请求受安全描述符保护的对象的提供程序，该安全描述符的 ACL 应基于输入 ACL，而不考虑其源 (显式还是默认情况下) 。 这是通过将所有 GRANT Ace 替换为授予当前服务器的复合 Ace 来完成的。 仅当使用者正在模拟时，此标志才有意义。</p></td>
</tr>
</tbody>
</table>

 

## <a name="requirements"></a>要求


ntifs (包含 ntifs) 

## <a name="related-topics"></a>相关主题


[**ACE**](ace.md)

[**ACL**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_acl)

[**RtlSetDaclSecurityDescriptor**](/windows-hardware/drivers/ddi/wdm/nf-wdm-rtlsetdaclsecuritydescriptor)

[**RtlSetOwnerSecurityDescriptor**](/windows-hardware/drivers/ddi/ntifs/nf-ntifs-rtlsetownersecuritydescriptor)

[**安全 \_ 描述符**](/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))

 

