---
title: GUID_NDIS_GEN_PCI_DEVICE_CUSTOM_PROPERTIES
description: WMI 客户端可以使用 GUID_NDIS_GEN_PCI_DEVICE_CUSTOM_PROPERTIES 方法 GUID 来确定当前的链接状态。
ms.assetid: a02b9049-e521-41df-ab4d-41e334ef779e
ms.date: 08/08/2017
keywords: -GUID_NDIS_GEN_PCI_DEVICE_CUSTOM_PROPERTIES 网络与 Windows Vista 一起启动的驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 565fa9634d9bd5a516b10e0179f8991588dd3229
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63361073"
---
# <a name="guidndisgenpcidevicecustomproperties"></a>GUID\_NDIS\_代\_PCI\_设备\_自定义\_属性


WMI 客户端可以使用的 GUID\_NDIS\_代\_PCI\_设备\_自定义\_属性方法以确定当前的链接状态的 GUID。

<a name="remarks"></a>备注
-------

NDIS 处理此 GUID 和微型端口驱动程序不会收到一个 OID 查询。

WMI 客户端时发出一个 GUID\_NDIS\_代\_PCI\_设备\_自定义\_属性 WMI 方法请求，NDIS 返回 PCI 的微型端口 PCI 设备的自定义属性适配器。 WMI 方法标识符应为 NDIS\_WMI\_默认\_方法\_ID 和 WMI 输入缓冲区应包含[ **NDIS\_WMI\_方法\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff567903)结构。

包含此 GUID 与的 NDIS 返回的数据缓冲区[ **NDIS\_PCI\_设备\_自定义\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff566745)结构。

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


[**NDIS\_PCI\_设备\_自定义\_属性**](https://msdn.microsoft.com/library/windows/hardware/ff566745)

[**NDIS\_WMI\_方法\_标头**](https://msdn.microsoft.com/library/windows/hardware/ff567903)

 

 




