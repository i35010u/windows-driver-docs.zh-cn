---
title: OID_GEN_PCI_DEVICE_CUSTOM_PROPERTIES
description: 为查询，基础驱动程序使用 OID_GEN_PCI_DEVICE_CUSTOM_PROPERTIES OID 获取 PCI 设备的自定义属性。
ms.assetid: fe94884b-f5e3-4c60-8f52-e61d0df81a2a
ms.date: 08/08/2017
keywords: -OID_GEN_PCI_DEVICE_CUSTOM_PROPERTIES 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b4682a1d13192db3a0cfe06dce88da1446a1dbda
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386220"
---
# <a name="oidgenpcidevicecustomproperties"></a>OID\_GEN\_PCI\_设备\_自定义\_属性


为查询，基础驱动程序使用 OID\_GEN\_PCI\_设备\_自定义\_属性 OID，若要获取设备的 PCI 自定义属性。

<a name="remarks"></a>备注
-------

NDIS 处理 OID\_GEN\_PCI\_设备\_自定义\_属性和微型端口驱动程序不会收到一个 OID 查询。

此查询是可选的其他 NDIS 驱动程序。

返回 NDIS [ **NDIS\_PCI\_设备\_自定义\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pci_device_custom_properties)结构，其中包含 PCI 的自定义属性。

对于非 PCI 微型端口适配器，NDIS 失败 OID\_GEN\_PCI\_设备\_自定义\_属性与的 NDIS\_状态\_无效\_设备\_请求状态代码。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>支持 NDIS 6.0 及更高版本。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ntddndis.h （包括 Ndis.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**NDIS\_PCI\_设备\_自定义\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_pci_device_custom_properties)

 

 




