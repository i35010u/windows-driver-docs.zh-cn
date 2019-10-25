---
title: OID_GEN_PCI_DEVICE_CUSTOM_PROPERTIES
description: 作为查询，过量驱动程序使用 OID_GEN_PCI_DEVICE_CUSTOM_PROPERTIES OID 获取设备的 PCI 自定义属性。
ms.assetid: fe94884b-f5e3-4c60-8f52-e61d0df81a2a
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 OID_GEN_PCI_DEVICE_CUSTOM_PROPERTIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: ded468b6321b33200058aa9cdb06575cb0760bbb
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824387"
---
# <a name="oid_gen_pci_device_custom_properties"></a>OID\_代\_PCI\_设备\_自定义\_属性


作为查询，过量驱动程序使用 OID\_代\_PCI\_设备\_自定义\_属性 OID 获取设备的 PCI 自定义属性。

<a name="remarks"></a>备注
-------

NDIS 处理 OID\_代\_PCI\_设备\_自定义\_属性和微型端口驱动程序未收到 OID 查询。

此查询对于其他 NDIS 驱动程序是可选的。

NDIS 返回[ **\_pci\_设备的 ndis，\_** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pci_device_custom_properties)包含 pci 自定义属性的自定义\_属性结构。

对于非 PCI 微型端口适配器，NDIS 会使 OID 失败\_代\_PCI\_设备\_自定义\_属性，其 NDIS\_状态\_无效\_设备\_请求状态代码。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>版本</p></td>
<td><p>在 NDIS 6.0 和更高版本中受支持。</p></td>
</tr>
<tr class="even">
<td><p>标头</p></td>
<td>Ntddndis （包括 Ndis .h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS\_PCI\_设备\_自定义\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pci_device_custom_properties)

 

 




