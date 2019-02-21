---
title: OID_GEN_MACHINE_NAME
description: 作为一组 OID_GEN_MACHINE_NAME OID 指示微型端口驱动程序将本地计算机名称。
ms.assetid: 771d21ff-e989-4717-8f3e-28f4b8afe274
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_MACHINE_NAME 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b08f79c86d00efd9930443c1ae8229b14ae7487f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533711"
---
# <a name="oidgenmachinename"></a>OID\_GEN\_MACHINE\_NAME


作为一组 OID\_GEN\_机\_名称 OID 指示微型端口驱动程序将本地计算机名称。

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

在此请求中传递的信息缓冲区包含表示本地计算机名称的 Unicode 字符数组。 **InformationBufferLength**提供给的值[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)函数指定此数组的长度以字节为单位，不包括 null 值终结器。

NDIS 设置 OID\_GEN\_机\_微型端口驱动程序完成初始化后一次命名。 在 Windows XP 下 NDIS 不会动态地通知微型端口驱动程序的计算机名称更改。 更改计算机名称后，用户必须重新启动计算机，以便 NDIS 通知新的计算机名称的微型端口驱动程序。

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


[*MiniportOidRequest*](https://msdn.microsoft.com/library/windows/hardware/ff559416)

 

 




