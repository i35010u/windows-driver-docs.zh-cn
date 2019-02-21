---
title: WDI_TLV_P2P_INVITATION_REQUEST_PARAMETERS
description: WDI_TLV_P2P_INVITATION_REQUEST_PARAMETERS 是 TLV 包含 Wi-Fi Direct 邀请请求参数。
ms.assetid: CC9B0454-4522-4589-8E21-4986BAEBC6D0
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_INVITATION_REQUEST_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: cac2e8c37aee93e87f664396de68dea854e321d0
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56523704"
---
# <a name="wditlvp2pinvitationrequestparameters"></a>WDI\_TLV\_P2P\_邀请\_请求\_参数


WDI\_TLV\_P2P\_邀请\_请求\_参数是包含 Wi-Fi Direct 邀请请求参数 TLV。

## <a name="tlv-type"></a>TLV 类型


0x7C

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>在任务栏的搜索框中键入</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT16</td>
<td>以毫秒为单位的组所有者配置超时。</td>
</tr>
<tr class="even">
<td>UINT16</td>
<td>客户端配置的超时以毫秒为单位。</td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>邀请标志由 Wi-Fi Direct 规范定义。</td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>位，指示传出的邀请请求是本地的组所有者的邀请。
<p>有效值为 0 和 1。 如果它是本地转到邀请此位设置为 1。</p></td>
</tr>
</tbody>
</table>

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




