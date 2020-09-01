---
title: GUID_DEVINTERFACE_BRIGHTNESS
description: GUID_DEVINTERFACE_BRIGHTNESS
ms.assetid: a31b4e12-3702-4a24-98c0-cf8ae7d86a75
keywords:
- GUID_DEVINTERFACE_BRIGHTNESS 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_BRIGHTNESS
api_location:
- Dispmprt.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: aabfca0b987ea090964e8dbf549b83c331997887
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097315"
---
# <a name="guid_devinterface_brightness"></a>GUID_DEVINTERFACE_BRIGHTNESS


为显示适配器驱动程序定义了 GUID_DEVINTERFACE_BRIGHTNESS [设备接口类](./overview-of-device-interface-classes.md) ，该驱动程序在 [Windows Vista 显示器驱动程序模型](../display/windows-vista-display-driver-model-design-guide.md) 的上下文中运行，并支持监视子设备的亮度控制。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">Attribute</th>
<th align="left">设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>标识符</p></td>
<td align="left"><p>GUID_DEVINTERFACE_BRIGHTNESS</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{FDE5BBA4-B3F9-46FB-BDAA-0728CE3100B4}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

驱动程序将注册此设备接口类的实例，通知操作系统和应用程序是否存在监视子设备的亮度控制接口。

如果显示微型端口驱动程序支持此 [设备安装程序类](./overview-of-device-setup-classes.md)的直接调用亮度控制接口，则内核模式组件可以通过调用微型端口驱动程序的 [**DxgkDdiQueryInterface**](/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface) 函数并提供 GUID_DEVINTERFACE_BRIGHTNESS 来指定接口类型，从而检索直接调用接口。

有关亮度设备的信息，请参阅在集成显示面板和[亮度控制界面](/windows-hardware/drivers/ddi/index)[上支持亮度控件](../display/supporting-brightness-controls-on-integrated-display-panels.md)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>版本</p></td>
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Dispmprt (包含 Dispmprt) </td>
</tr>
</tbody>
</table>

 

