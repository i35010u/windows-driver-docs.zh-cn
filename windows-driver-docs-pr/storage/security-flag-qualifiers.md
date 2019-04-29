---
title: 安全\_标志\_限定符
description: 安全\_标志\_限定符
ms.assetid: d5b4c3a6-1e05-497a-a0a6-be7908e61fec
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a7dfeebe177b90fbf5a0814b278b33e1d471f571
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356715"
---
# <a name="securityflagqualifiers"></a>安全\_标志\_限定符


## <span id="ddk_security_flag_qualifiers_kr"></span><span id="DDK_SECURITY_FLAG_QUALIFIERS_KR"></span>


安全性\_标志\_限定符 WMI 属性限定符对应于标志值，用于指示目标的安全要求。 此信息用于在 IPsec 身份验证协商 Internet 密钥交换 (IKE)。 这些标志派生自中所述的门户安全位图定义*Internet 存储名称服务 (iSNS)* Internet 工程任务组 (IETF) 发布的规范。

下表描述了与安全相关联的值\_标志\_限定符属性限定符。

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
<td align="left"><p>目标请求隧道模式。 HBA 发起程序应登录到目标使用 IPsec 隧道模式。 如果未设置此值，则不需要 IPsec 隧道模式。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISCSI_SECURITY_FLAG_TRANSPORT_MODE_PREFERRED</p></td>
<td align="left"><p>目标请求传输模式。 HBA 发起程序应登录到目标使用 IPsec 传输模式。 如果未设置此值，则不需要 IPsec 传输模式。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISCSI_SECURITY_FLAG_PFS_ENABLED</p></td>
<td align="left"><p>HBA 发起程序应使用登录到目标已启用完全向前保密 (PFS) 模式。 如果未设置此值，发起方 HBA 应 PFS 模式下禁用请会话连接。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISCSI_SECURITY_FLAG_AGGRESSIVE_MODE_ENABLED</p></td>
<td align="left"><p>在目标上启用主动模式和 HBA 发起程序应使用登录到目标启用了主动模式。 时未设置此值，HBA 发起程序应该主动模式下禁用建立会话连接。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISCSI_SECURITY_FLAG_MAIN_MODE_ENABLED</p></td>
<td align="left"><p>在目标上启用主模式和 HBA 发起程序应使用登录到目标启用的主模式。 未设置时，HBA 发起程序应使用禁用的主模式建立会话连接。</p></td>
</tr>
<tr class="even">
<td align="left"><p>ISCSI_SECURITY_FLAG_IKE_IPSEC_ENABLED</p></td>
<td align="left"><p>IKE/IPsec 启用对目标和 HBA 发起程序应使用登录到目标启用的 IKE/IPsec 协议。 如果未设置此值，IKE/IPsec 已禁用。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>ISCSI_SECURITY_FLAG_VALID</p></td>
<td align="left"><p>此位掩码中指定的 iSCSI 安全标志是有效的。 如果未设置此值，未指定安全标志。</p></td>
</tr>
</tbody>
</table>

 

 

 





