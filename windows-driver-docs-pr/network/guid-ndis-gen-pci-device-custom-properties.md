---
title: GUID_NDIS_GEN_PCI_DEVICE_CUSTOM_PROPERTIES
description: WMI 客户端可以使用 GUID_NDIS_GEN_PCI_DEVICE_CUSTOM_PROPERTIES 方法 GUID 来确定当前链接状态。
ms.assetid: a02b9049-e521-41df-ab4d-41e334ef779e
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 GUID_NDIS_GEN_PCI_DEVICE_CUSTOM_PROPERTIES 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 60970160dc2044c8523f11e937cbcbaa536e254b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842293"
---
# <a name="guid_ndis_gen_pci_device_custom_properties"></a>GUID\_NDIS\_GEN\_PCI\_设备\_自定义\_属性


WMI 客户端可以使用 GUID\_NDIS\_GEN\_PCI\_设备\_自定义\_属性方法 GUID 来确定当前链接状态。

<a name="remarks"></a>备注
-------

NDIS 处理此 GUID 和微型端口驱动程序不会收到 OID 查询。

当 WMI 客户端\_NDIS\_生成 GUID 时\_PCI\_设备\_自定义\_属性 WMI 方法请求，NDIS 为微型端口适配器返回 PCI 设备的 PCI 自定义属性。 WMI 方法标识符应为 NDIS\_WMI\_默认\_方法\_ID，WMI 输入缓冲区应包含[**ndis\_wmi\_方法\_标题**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_method_header)结构。

NDIS 使用此 GUID 返回的数据缓冲区包含一个[**NDIS\_PCI\_设备\_自定义\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pci_device_custom_properties)结构。

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

[**NDIS\_WMI\_方法\_标头**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_method_header)

 

 




