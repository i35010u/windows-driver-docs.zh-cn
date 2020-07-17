---
title: DEVPKEY_Device_InstallState
description: DEVPKEY_Device_InstallState
ms.assetid: 3bebb3d6-96bb-4c7c-8a7a-c5bf29cb3a2a
keywords:
- DEVPKEY_Device_InstallState 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_InstallState
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 4fabf1b03bb475a98d916f401e9310c52a65e6b4
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418281"
---
# <a name="devpkey_device_installstate"></a>DEVPKEY_Device_InstallState


DEVPKEY_Device_InstallState 设备属性表示设备实例的安装状态。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr>
<th>属性</th>
<th>Value</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_InstallState</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-uint32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_UINT32&lt;/strong&gt;](devprop-type-uint32.md)"><strong>DEVPROP_TYPE_UINT32</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>由安装应用程序和安装程序只读</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>对应 SPDRP_</strong><em>Xxx</em> <strong>标识符</strong></p></td>
<td align="left"><p>SPDRP_INSTALL_STATE</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

Windows 将 DEVPKEY_Device_InstallState 的值设置为 Cfgmgr32 中定义的 CM_INSTALL_STATE_*Xxx*值之一。 CM_INSTALL_STATE_*Xxx*值对应于[**DEVICE_INSTALL_STATE**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/ne-wdm-_device_install_state)枚举值。

可以调用[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)来检索 DEVPKEY_Device_InstallState 的值。

Windows Server 2003 和 Windows XP 支持此属性，但不支持 DEVPKEY_Device_InstallState 属性键。 相反，你可以使用相应的 SPDRP_INSTALL_STATE 标识符来访问这些早期版本的 Windows 上的属性值。 有关如何在这些早期版本的 Windows 上访问此属性值的信息，请参阅[SPDRP_Xxx 属性访问设备实例](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-instance-spdrp-xxx-properties)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows**头**： Devpkey （包括 Devpkey）


## <a name="see-also"></a>请参阅


[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






