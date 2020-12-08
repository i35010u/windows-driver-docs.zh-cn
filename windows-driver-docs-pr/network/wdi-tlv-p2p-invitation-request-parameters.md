---
title: WDI_TLV_P2P_INVITATION_REQUEST_PARAMETERS
description: WDI_TLV_P2P_INVITATION_REQUEST_PARAMETERS 是包含 Wi-Fi 直接邀请请求参数的 TLV。
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_P2P_INVITATION_REQUEST_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b4348d5757f5ba6ea72e99157300271da408563a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818235"
---
# <a name="wdi_tlv_p2p_invitation_request_parameters"></a>WDI \_ TLV \_ P2P \_ 邀请 \_ 请求 \_ 参数


WDI \_ tlv \_ P2P \_ 邀请 \_ 请求 \_ 参数是包含 Wi-Fi 直接邀请请求参数的 tlv。

## <a name="tlv-type"></a>TLV 类型


0x7C

## <a name="length"></a>长度


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>类型</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>UINT16</td>
<td>组所有者配置超时（以毫秒为单位）。</td>
</tr>
<tr class="even">
<td>UINT16</td>
<td>客户端配置超时（以毫秒为单位）。</td>
</tr>
<tr class="odd">
<td>UINT8</td>
<td>由 Wi-Fi 直接规范定义的邀请标志。</td>
</tr>
<tr class="even">
<td>UINT8</td>
<td>指示传出邀请请求是否为本地组所有者邀请的一个位。
<p>有效值为0和1。 如果此位是对本地旅途的邀请，则设置为1。</p></td>
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
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




