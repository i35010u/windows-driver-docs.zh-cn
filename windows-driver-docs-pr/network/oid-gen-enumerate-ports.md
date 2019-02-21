---
title: OID_GEN_ENUMERATE_PORTS
description: 为查询，NDIS 和基础驱动程序使用 OID_GEN_ENUMERATE_PORTS OID 来确定活动的 NDIS 端口与基础的微型端口适配器关联的特征。
ms.assetid: 42a12a05-e360-4493-b037-d3a63906a132
ms.date: 08/08/2017
keywords: -OID_GEN_ENUMERATE_PORTS 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: d6b622ba3d331a92898e07e07d55233ebaff71a8
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56541797"
---
# <a name="oidgenenumerateports"></a>OID\_GEN\_ENUMERATE\_端口


为查询，NDIS 和基础驱动程序使用 OID\_GEN\_ENUMERATE\_端口 OID，以确定活动的 NDIS 端口与基础的微型端口适配器关联的特征。

**版本信息**

<a href="" id="windows-vista-and-later-versions-of-windows"></a>Windows Vista 和更高版本的 Windows  
支持。

<a href="" id="ndis-6-0-and-later-miniport-drivers"></a>NDIS 6.0 和更高版本的微型端口驱动程序  
未请求。 (请参阅备注部分)

<a name="remarks"></a>备注
-------

NDIS 处理此 OID 和微型端口驱动程序不会收到此 OID 查询。

如果查询成功，NDIS 返回 NDIS\_状态\_成功，并提供在查询的结果[ **NDIS\_端口\_数组**](https://msdn.microsoft.com/library/windows/hardware/ff566786)结构. **NumberOfPorts**成员的 NDIS\_端口\_数组包含的活动与微型端口适配器关联的端口号。 **端口**成员的 NDIS\_端口\_数组包含指向的指针的列表[ **NDIS\_端口\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff566791)结构。 每个 NDIS\_端口\_特征结构定义单个 NDIDS 端口的特征。

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


[**NDIS\_端口\_数组**](https://msdn.microsoft.com/library/windows/hardware/ff566786)

[**NDIS\_端口\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff566791)

 

 




