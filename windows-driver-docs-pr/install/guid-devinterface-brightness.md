---
title: GUID_DEVINTERFACE_BRIGHTNESS
description: GUID_DEVINTERFACE_BRIGHTNESS
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
ms.openlocfilehash: 689426986fca4e38b8c08fc4c709ac5b34011c1b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813135"
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

有关亮度设备的信息，请参阅在集成显示面板和[亮度控制界面]()[上支持亮度控件](../display/supporting-brightness-controls-on-integrated-display-panels.md)。

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

 

