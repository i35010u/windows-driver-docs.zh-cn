---
title: OID_GEN_MACHINE_NAME
description: OID_GEN_MACHINE_NAME OID 将本地计算机名称指定为微型端口驱动程序。
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_MACHINE_NAME 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 56e3659645095c3f79acb1f0e8fac3e92d6fc51b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822177"
---
# <a name="oid_gen_machine_name"></a>OID \_ 生成 \_ 计算机 \_ 名称


作为一个集，OID 生成 \_ \_ 计算机 \_ 名称 oid 将本地计算机名称指定为微型端口驱动程序。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
可选。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
可选。

<a href="" id="windows-xp"></a>Windows XP  
支持。

<a href="" id="ndis-5-1-miniport-drivers"></a>NDIS 5.1 微型端口驱动程序  
可选。

<a name="remarks"></a>备注
-------

传入此请求的信息缓冲区包含表示本地计算机名称的 Unicode 字符数组。 提供给 [*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)函数的 **InformationBufferLength** 值指定此数组的长度（以字节为单位），不包括 NULL 终止符。

在 \_ \_ \_ 微型端口驱动程序完成初始化后，NDIS 仅设置 OID 生成计算机名称一次。 在 Windows XP 下，NDIS 不会动态通知小型端口驱动程序的计算机名称更改。 更改计算机名后，用户必须重新启动计算机，以便 NDIS 通知小型端口驱动程序的新计算机名。

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


[*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)

 

