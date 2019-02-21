---
title: OID_GEN_PORT_AUTHENTICATION_PARAMETERS
description: 作为一组 NDIS 和基础驱动程序使用 OID_GEN_PORT_AUTHENTICATION_PARAMETERS OID 来设置 NDIS 端口的当前状态。
ms.assetid: 676601c1-2647-4341-9a5c-cee895d2dbf7
ms.date: 08/08/2017
keywords: -OID_GEN_PORT_AUTHENTICATION_PARAMETERS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: dcc74e0a1d5ef936c94d51c50547d91270fa0a45
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541741"
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

如果微型端口驱动程序支持此 OID，驱动程序将返回 NDIS\_状态\_成功并提供接收端口方向、 端口控件状态，并进行身份验证中的状态[ **NDIS\_端口\_身份验证\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566788)结构。

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
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_端口\_身份验证\_参数**](https://msdn.microsoft.com/library/windows/hardware/ff566788)

 

 




