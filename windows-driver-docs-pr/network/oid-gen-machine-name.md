---
title: OID_GEN_MACHINE_NAME
description: 作为一组，OID_GEN_MACHINE_NAME OID 会将本地计算机名称指定为微型端口驱动程序。
ms.assetid: 771d21ff-e989-4717-8f3e-28f4b8afe274
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_MACHINE_NAME 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 74d92e7df9a4d41bb4cd95620a4084a34c034638
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72843070"
---
# <a name="oid_gen_machine_name"></a>OID\_代\_计算机\_名称


作为一个集，OID\_代\_计算机\_名称 OID 指示到微型端口驱动程序的本地计算机名称。

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

传入此请求的信息缓冲区包含表示本地计算机名称的 Unicode 字符数组。 提供给[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)函数的**InformationBufferLength**值指定此数组的长度（以字节为单位），不包括 NULL 终止符。

在微型端口驱动程序完成初始化后，NDIS\_代\_计算机\_名称中设置 OID。 在 Windows XP 下，NDIS 不会动态通知小型端口驱动程序的计算机名称更改。 更改计算机名后，用户必须重新启动计算机，以便 NDIS 通知小型端口驱动程序的新计算机名。

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


[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)

 

 




