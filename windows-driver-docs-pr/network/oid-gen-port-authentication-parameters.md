---
title: OID_GEN_PORT_AUTHENTICATION_PARAMETERS
description: 作为集，NDIS 和过量驱动程序使用 OID_GEN_PORT_AUTHENTICATION_PARAMETERS OID 设置 NDIS 端口的当前状态。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_PORT_AUTHENTICATION_PARAMETERS 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 67002ae168b8bbc8576834cab9fca7a1fe0020f9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829445"
---
# <a name="oid_gen_port_authentication_parameters"></a>OID \_ GEN \_ 端口 \_ 身份验证 \_ 参数


作为集，NDIS 和过量驱动程序使用 OID \_ GEN \_ 端口 \_ 身份验证 \_ 参数 OID 设置 NDIS 端口的当前状态。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
可选。 对于 NDIS 端口是必需的。  (参见 "备注" 部分) 

<a name="remarks"></a>备注
-------

支持 NDIS 端口的微型端口驱动程序必须支持此 OID。

如果微型端口驱动程序不支持此 OID，微型端口驱动程序应返回 \_ \_ 不 \_ 受支持的 NDIS 状态。

如果微型端口驱动程序支持此 OID，则驱动程序将返回 NDIS \_ 状态 \_ 成功，并在 [**NDIS \_ 端口 \_ 身份验证 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_authentication_parameters) 结构中提供接收端口方向、端口控制状态和身份验证状态。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS \_ 端口 \_ 身份验证 \_ 参数**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_authentication_parameters)

 

