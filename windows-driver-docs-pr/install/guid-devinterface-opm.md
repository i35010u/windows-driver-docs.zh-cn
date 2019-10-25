---
title: GUID_DEVINTERFACE_OPM
description: GUID_DEVINTERFACE_OPM
ms.assetid: bd999b09-d531-4b89-a306-83e1ca7cac64
keywords:
- GUID_DEVINTERFACE_OPM 设备和驱动程序安装
topic_type:
- apiref
api_name:
- GUID_DEVINTERFACE_OPM
api_location:
- Dispmprt.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: e8374b9a01e61e13da9b06482156b710f7cadf42
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840635"
---
# <a name="guid_devinterface_opm"></a>GUID_DEVINTERFACE_OPM


为显示适配器驱动程序定义 GUID_DEVINTERFACE_OPM[设备接口类](https://docs.microsoft.com/windows-hardware/drivers/install/device-interface-classes)，该驱动程序在[Windows Vista 显示器驱动程序模型](https://docs.microsoft.com/windows-hardware/drivers/display/windows-vista-display-driver-model-design-guide)的上下文中运行，并支持监视子设备的输出保护管理（OPM）。

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
<td align="left"><p>GUID_DEVINTERFACE_OPM</p></td>
</tr>
<tr class="even">
<td align="left"><p>类 GUID</p></td>
<td align="left"><p>{BF4672DE-6B4E-4BE4-A325-68A91EA49C09}</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

驱动程序将注册此设备接口类的实例，通知操作系统和应用程序是否存在 OPM 设备接口。

如果显示微型端口驱动程序支持此[设备安装程序类](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)的直接调用 OPM 接口，则内核模式组件可以通过调用微型端口驱动程序的[**DxgkDdiQueryInterface**](https://docs.microsoft.com/windows-hardware/drivers/ddi/dispmprt/nc-dispmprt-dxgkddi_query_interface)函数并提供GUID_DEVINTERFACE_OPM 指定接口类型。

有关 OPM 的信息，请参阅[支持输出保护管理器](https://docs.microsoft.com/windows-hardware/drivers/display/supporting-output-protection-manager)。

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

 

 





