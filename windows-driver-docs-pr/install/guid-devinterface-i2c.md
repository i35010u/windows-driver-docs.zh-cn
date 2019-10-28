---
title: GUID_DEVINTERFACE_I2C
description: GUID_DEVINTERFACE_I2C
ms.assetid: 765cecb7-b8ea-48ef-bdab-742da722e169
keywords:
- GUID_DEVINTERFACE_I2C 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_I2C
api_location:
- Dispmprt.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 89e950f8c734fb491a204b5a383ac21e87a1bdbe
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840630"
---
# <a name="guid_devinterface_i2c"></a>GUID_DEVINTERFACE_I2C


为显示适配器驱动程序定义 GUID_DEVINTERFACE_I2C[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)，该驱动程序在[Windows Vista 显示驱动程序模型](https://docs.microsoft.com/windows-hardware/drivers/display/windows-vista-display-driver-model-design-guide)的上下文中运行，并通过监视子设备执行 I2C 事务。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">属性</th>
<th align="left">设置</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>标识符</p></td>
<td align="left"><p>GUID_DEVINTERFACE_I2C</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{2564AA4F-DDDB-4495-B497-6AD4A84163D7}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

驱动程序将注册此设备接口类的实例，以通知操作系统和应用程序是否存在通过监视子设备执行事务的 I2C 接口。

如果显示微型端口驱动程序支持此[设备安装程序类](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)的直接调用 I2C 接口，则内核模式组件可以通过调用微型端口驱动程序的[**DxgkDdiQueryInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface)函数并提供GUID_DEVINTERFACE_I2C 指定接口类型。

有关 I2C 总线的信息，请参阅[显示适配器的 I2C 总线和子设备](https://docs.microsoft.com/windows-hardware/drivers/display/i2c-bus-and-child-devices-of-the-display-adapter)。

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
<td align="left">Dispmprt （包括 Dispmprt）</td>
</tr>
</tbody>
</table>

 

 





