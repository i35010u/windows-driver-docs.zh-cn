---
title: 安全 \_ 标志 \_ 限定符
description: 安全 \_ 标志 \_ 限定符
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: c39338ace5e60aa64d6c8899be755c851d1cebf3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839389"
---
# <a name="security_flag_qualifiers"></a>安全 \_ 标志 \_ 限定符


## <span id="ddk_security_flag_qualifiers_kr"></span><span id="DDK_SECURITY_FLAG_QUALIFIERS_KR"></span>


安全 \_ 标志 \_ 限定符 WMI 属性限定符对应于指示目标的安全要求的标志值。 此信息用于 IPsec 身份验证协商 (IKE) Internet 密钥交换。 这些标志派生自 internet *存储名称服务 (iSNS)* 规范（Internet 工程任务组 (IETF) 发布）中所述的门户安全位图定义。

下表描述了与安全 \_ 标志 \_ 限定符属性限定符关联的值。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">符号常量</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ISCSI_SECURITY_FLAG_TUNNEL_MODE_PREFERRED</p></td>
<td align="left"><p>目标请求隧道模式。 HBA 发起程序应使用 IPsec 隧道模式登录到目标。 如果未设置此值，则不需要 IPsec 隧道模式。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISCSI_SECURITY_FLAG_TRANSPORT_MODE_PREFERRED</p></td>
<td align="left"><p>目标请求传输模式。 HBA 发起程序应使用 IPsec 传输模式登录到目标。 如果未设置此值，则不需要 IPsec 传输模式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISCSI_SECURITY_FLAG_PFS_ENABLED</p></td>
<td align="left"><p>HBA 发起方应以完全向前保密 (PFS) 模式登录到目标。 如果未设置此值，则发起方 HBA 应使会话连接的 PFS 模式处于禁用状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISCSI_SECURITY_FLAG_AGGRESSIVE_MODE_ENABLED</p></td>
<td align="left"><p>在目标上启用了积极模式，并且 HBA 发起程序应登录到启用了积极模式的目标。 如果未设置此值，则 HBA 发起程序应使会话连接处于禁用状态。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISCSI_SECURITY_FLAG_MAIN_MODE_ENABLED</p></td>
<td align="left"><p>在目标上启用主模式，并且 HBA 发起程序应登录到启用了主模式的目标。 如果未设置，则 HBA 发起程序应使会话连接处于禁用状态。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISCSI_SECURITY_FLAG_IKE_IPSEC_ENABLED</p></td>
<td align="left"><p>在目标上启用了 IKE/IPsec，并且 HBA 发起程序应登录到启用了 IKE/IPsec 协议的目标。 如果未设置此值，将禁用 IKE/IPsec。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISCSI_SECURITY_FLAG_VALID</p></td>
<td align="left"><p>此位掩码中指定的 iSCSI 安全标志是有效的。 如果未设置此值，则不指定安全标志。</p></td>
</tr>
</tbody>
</table>

 

 

 





