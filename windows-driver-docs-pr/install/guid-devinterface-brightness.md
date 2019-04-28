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
ms.openlocfilehash: 519315cf1c00d4e3d2e0561821bd671f4de6daee
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63342060"
---
# <a name="guiddevinterfacebrightness"></a>GUID_DEVINTERFACE_BRIGHTNESS


GUID_DEVINTERFACE_BRIGHTNESS[设备接口类](https://msdn.microsoft.com/library/windows/hardware/ff541339)显示适配器驱动程序的上下文中运行，为定义[Windows Vista 显示器驱动程序模型](https://msdn.microsoft.com/library/windows/hardware/ff570593)和支持的亮度控制监视子设备。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">特性</th>
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

驱动程序注册通知的操作系统和应用程序的亮度控制接口的监视器子设备存在此设备接口类的实例。

如果显示微型端口驱动程序支持直接调用亮度控制接口的这[设备安装程序类](https://msdn.microsoft.com/library/windows/hardware/ff541509)，内核模式组件可以通过调用微型端口驱动程序检索直接调用接口[ **DxgkDdiQueryInterface** ](https://msdn.microsoft.com/library/windows/hardware/ff559764)函数并提供 GUID_DEVINTERFACE_BRIGHTNESS 指定接口类型。

亮度设备有关的信息，请参阅[支持集成显示器的亮度控件](https://msdn.microsoft.com/library/windows/hardware/ff569755)并[亮度控制接口](https://msdn.microsoft.com/library/windows/hardware/ff538260)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Windows Vista 和更高版本的 Windows 中可用。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Dispmprt.h （包括 Dispmprt.h）</td>
</tr>
</tbody>
</table>

 

 





