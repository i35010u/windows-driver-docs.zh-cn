---
title: OID_GEN_PORT_AUTHENTICATION_PARAMETERS
description: 作为集，NDIS 和过量驱动程序使用 OID_GEN_PORT_AUTHENTICATION_PARAMETERS OID 设置 NDIS 端口的当前状态。
ms.assetid: 676601c1-2647-4341-9a5c-cee895d2dbf7
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_PORT_AUTHENTICATION_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 193e189fbfd9ac0081f87b864852b7896932d3c7
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824383"
---
# <a name="oid_gen_port_authentication_parameters"></a>OID\_代\_端口\_AUTHENTICATION\_参数


作为集，NDIS 和过量驱动程序使用 OID\_代\_端口\_AUTHENTICATION\_参数 OID 设置 NDIS 端口的当前状态。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
可选。 对于 NDIS 端口是必需的。 （请参见 "备注" 部分）

<a name="remarks"></a>备注
-------

支持 NDIS 端口的微型端口驱动程序必须支持此 OID。

如果微型端口驱动程序不支持此 OID，微型端口驱动程序应返回 NDIS\_状态\_不\_支持。

如果微型端口驱动程序支持此 OID，则驱动程序将\_状态返回 NDIS\_状态，并在[**NDIS\_端口\_AUTHENTICATION\_参数中提供接收端口方向、端口控制状态和身份验证状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_authentication_parameters)结构。

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
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_端口\_身份验证\_参数**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_port_authentication_parameters)

 

 




