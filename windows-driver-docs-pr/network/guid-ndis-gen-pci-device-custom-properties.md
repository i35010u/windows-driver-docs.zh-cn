---
title: GUID_NDIS_GEN_PCI_DEVICE_CUSTOM_PROPERTIES
description: WMI 客户端可以使用 GUID_NDIS_GEN_PCI_DEVICE_CUSTOM_PROPERTIES 方法 GUID 来确定当前链接状态。
ms.assetid: a02b9049-e521-41df-ab4d-41e334ef779e
ms.date: 08/08/2017
keywords: -从 Windows Vista 开始 GUID_NDIS_GEN_PCI_DEVICE_CUSTOM_PROPERTIES 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 416389bd96136c5cc41e05b7f59bf6a4b46f9ad4
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89217636"
---
# <a name="guid_ndis_gen_pci_device_custom_properties"></a>GUID \_ NDIS \_ 生成 \_ PCI \_ 设备 \_ 自定义 \_ 属性


WMI 客户端可以使用 GUID \_ NDIS \_ 生成 \_ PCI \_ 设备 \_ 自定义 \_ 属性方法 guid 来确定当前链接状态。

<a name="remarks"></a>备注
-------

NDIS 处理此 GUID 和微型端口驱动程序不会收到 OID 查询。

当 WMI 客户端发出 GUID \_ NDIS 生成 \_ \_ PCI \_ 设备 \_ 自定义 \_ 属性 WMI 方法请求时，NDIS 将为微型端口适配器返回 pci 设备的 pci 自定义属性。 WMI 方法标识符应为 NDIS \_ wmi \_ 默认 \_ 方法 \_ ID，wmi 输入缓冲区应包含 [**ndis \_ wmi \_ 方法 \_ 标头**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_method_header) 结构。

NDIS 返回的具有此 GUID 的数据缓冲区包含 [**ndis \_ PCI \_ 设备 \_ 自定义 \_ 属性**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pci_device_custom_properties) 结构。

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
<td>Ntddndis (包含 Ndis .h) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**NDIS \_ PCI \_ 设备 \_ 自定义 \_ 属性**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_pci_device_custom_properties)

[**NDIS \_ WMI \_ 方法 \_ 头**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_wmi_method_header)

 

