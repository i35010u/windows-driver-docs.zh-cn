---
title: OID_GEN_PORT_AUTHENTICATION_PARAMETERS
description: 作为一组 NDIS 和基础驱动程序使用 OID_GEN_PORT_AUTHENTICATION_PARAMETERS OID 来设置 NDIS 端口的当前状态。
ms.assetid: 676601c1-2647-4341-9a5c-cee895d2dbf7
ms.date: 08/08/2017
keywords: -OID_GEN_PORT_AUTHENTICATION_PARAMETERS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 9b2230aee48474c366ff83bceec56be8b535b084
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380862"
---
# <a name="oidgenportauthenticationparameters"></a>OID\_GEN\_端口\_身份验证\_参数


作为一组 NDIS 和基础驱动程序使用 OID\_GEN\_端口\_身份验证\_参数 OID 以设置 NDIS 端口的当前状态。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
可选。 对于 NDIS 端口是必需的。 (请参阅备注部分)

<a name="remarks"></a>备注
-------

支持 NDIS 端口的微型端口驱动程序必须支持此 OID。

如果微型端口驱动程序不支持此 OID，微型端口驱动程序应返回 NDIS\_状态\_不\_受支持。

如果微型端口驱动程序支持此 OID，驱动程序将返回 NDIS\_状态\_成功并提供接收端口方向、 端口控件状态，并进行身份验证中的状态[ **NDIS\_端口\_身份验证\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_authentication_parameters)结构。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_端口\_身份验证\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_port_authentication_parameters)

 

 




