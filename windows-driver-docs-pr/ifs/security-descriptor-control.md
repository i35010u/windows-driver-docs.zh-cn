---
title: 安全\_描述符\_控件
description: 安全\_描述符\_控件
ms.assetid: 6a7fe617-156d-4eb0-83f7-df78104acbde
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3739184af0f8c1c972f523d61683bddfe28e9483
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371337"
---
# <a name="securitydescriptorcontrol"></a>安全\_描述符\_控件


**安全\_描述符\_控件**类型是一组位标志，用于限定的含义[**安全\_描述符**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))结构或其组件。 每个安全描述符**控制**成员将存储**安全\_描述符\_控制**位。

安全\_描述符\_控件

``` syntax
typedef USHORT SECURITY_DESCRIPTOR_CONTROL, *PSECURITY_DESCRIPTOR_CONTROL;
```

控件的值可以包含的以下组合**安全\_描述符\_控制**位标志：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">ReplTest1</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>SE_DACL_AUTO_INHERIT_REQ</p></td>
<td align="left"><p>请求的提供程序自动保护的安全描述符的对象将传播到现有的子对象的 DACL。 如果提供程序支持自动继承，它将传播到任何现有的子对象的 DACL，并设置 SE_DACL_AUTO_INHERITED 位中的安全描述符的对象及其子对象。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_DACL_AUTO_INHERITED</p></td>
<td align="left"><p>从 Windows 2000 中，指示在其中 DACL 支持自动传播到现有的子对象的可继承 Ace 的安全描述符。</p>
<p>对于支持自动继承的 Windows 2000 Acl，始终设置此位。 它用于将这些 Acl 与不支持自动继承的 Windows NT 4.0 Acl 区分开来。</p>
<p>在不支持的可继承 Ace 自动传播的安全描述符的 Windows NT 4.0 及更早版本，未设置此位。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SE_DACL_DEFAULTED</p></td>
<td align="left"><p>指示默认的 DACL 的安全描述符。 例如，如果对象的创建者未指定 DACL，该对象创建者的访问令牌从接收默认的 DACL。 此标志会影响系统处理的 DACL，相对于 ACE 继承的方式。 如果未设置 SE_DACL_PRESENT 标志，系统会忽略此标志。</p>
<p>此标志用于确定对象上的最终 DACL 的计算方式并不安全对象的安全描述符控制中以物理方式存储。</p>
<p>若要设置此标志，请使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlsetdaclsecuritydescriptor" data-raw-source="[&lt;strong&gt;RtlSetDaclSecurityDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlsetdaclsecuritydescriptor)"> <strong>RtlSetDaclSecurityDescriptor</strong></a>。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_DACL_PRESENT</p></td>
<td align="left"><p>指示具有 DACL 的安全描述符。 如果未设置此标志，或设置此标志且 DACL <strong>NULL</strong>，安全描述符允许对每个人都完全访问权限。</p>
<p>此标志用于保存与某个安全对象相关联的安全描述符之前由调用方指定的安全信息。 与安全对象相关联的安全描述符后，SE_DACL_PRESENT 标志始终设置中的安全描述符控制。</p>
<p>若要设置此标志，请使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlsetdaclsecuritydescriptor" data-raw-source="[&lt;strong&gt;RtlSetDaclSecurityDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlsetdaclsecuritydescriptor)"> <strong>RtlSetDaclSecurityDescriptor</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SE_DACL_PROTECTED</p></td>
<td align="left"><p>可继承 Ace 被修改，可保护的安全描述符的 DACL。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_DACL_UNTRUSTED</p></td>
<td align="left"><p>指示由受信任的源提供指向的安全描述符的 DACL 的 ACL。 如果设置此标志，并且遇到复合 ACE，系统将替换已知的 Sid 的 Ace 中的服务器的有效 Sid。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SE_GROUP_DEFAULTED</p></td>
<td align="left"><p>默认的机制，而不是原始提供程序的安全描述符，提供的安全描述符的组 SID。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_OWNER_DEFAULTED</p></td>
<td align="left"><p>默认的机制，而不是原始提供程序的安全描述符，提供安全描述符的所有者安全标识符 (SID)。 若要设置此标志，请使用<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-rtlsetownersecuritydescriptor" data-raw-source="[&lt;strong&gt;RtlSetOwnerSecurityDescriptor&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-rtlsetownersecuritydescriptor)"> <strong>RtlSetOwnerSecurityDescriptor</strong></a>。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SE_RM_CONTROL_VALID</p></td>
<td align="left"><p>指示的安全描述符中的资源控制管理器位有效。 资源管理器控制位是八位<strong>Sbz1</strong>的成员<a href="https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556610(v=vs.85)" data-raw-source="[&lt;strong&gt;SECURITY_DESCRIPTOR&lt;/strong&gt;](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))"> <strong>SECURITY_DESCRIPTOR</strong> </a>结构，其中包含特定于资源的信息访问结构管理器。 （有关详细信息，请参阅 Microsoft Windows 软件开发工具包 (SDK) for Windows 7 和.NET Framework 4.0 文档）。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_SACL_AUTO_INHERIT_REQ</p></td>
<td align="left"><p>请求的提供程序自动保护的安全描述符的对象将传播到现有的子对象的 SACL。 如果提供程序支持自动继承，它将传播到任何现有的子对象的 SACL 和 SE_SACL_AUTO_INHERITED 位设置中的安全描述符的对象及其子对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SE_SACL_AUTO_INHERITED</p></td>
<td align="left"><p>指示在其中 SACL 支持自动传播到现有的子对象的可继承 Ace 的安全描述符。 仅当已为对象和其现有的子对象执行自动继承算法，将设置此位。</p>
<p>在不支持的可继承 Ace 自动传播的安全描述符的 Windows NT 4.0 及更早版本，未设置此位。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_SACL_DEFAULTED</p></td>
<td align="left"><p>默认的机制，而不是原始提供程序的安全描述符，提供的 SACL。 此标志会影响系统处理的 SACL，相对于 ACE 继承的方式。 如果未设置 SE_SACL_PRESENT 标志，系统会忽略此标志。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SE_SACL_PRESENT</p></td>
<td align="left"><p>指示了 sacl 的安全描述符。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_SACL_PROTECTED</p></td>
<td align="left"><p>可继承 Ace 被修改，可保护的安全描述符的 SACL。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>SE_SELF_RELATIVE</p></td>
<td align="left"><p>指示自相关格式中的连续内存块中的所有安全信息的安全描述符。 如果未设置此标志，安全描述符的绝对格式。 有关详细信息，请参阅 Windows SDK 文档中的"绝对和 Self-Relative 安全描述符"。</p></td>
</tr>
<tr class="even">
<td align="left"><p>SE_SERVER_SECURITY</p></td>
<td align="left"><p>请求，该对象的提供程序保护的安全描述符的 ACL 应 ACL 基于输入 ACL，而不考虑其源 （显式或默认设置） 的服务器。 这是通过将所有授予 Ace 替换复合 Ace 授予当前服务器。 此标志才有意义，如果使用者正在模拟。</p></td>
</tr>
</tbody>
</table>

 

## <a name="requirements"></a>要求


ntifs.h （包括 ntifs.h）

## <a name="related-topics"></a>相关主题


[**ACE**](ace.md)

[**ACL**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_acl)

[**RtlSetDaclSecurityDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-rtlsetdaclsecuritydescriptor)

[**RtlSetOwnerSecurityDescriptor**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntifs/nf-ntifs-rtlsetownersecuritydescriptor)

[**安全\_描述符**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff556610(v=vs.85))

 

 






