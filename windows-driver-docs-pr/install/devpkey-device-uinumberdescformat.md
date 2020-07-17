---
title: DEVPKEY_Device_UINumberDescFormat
description: DEVPKEY_Device_UINumberDescFormat
ms.assetid: 6720b35e-a65b-4935-8010-aef53e3951e9
keywords:
- DEVPKEY_Device_UINumberDescFormat 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_UINumberDescFormat
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ba340256a64916119135c0910d5e7e701c402075
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418231"
---
# <a name="devpkey_device_uinumberdescformat"></a>DEVPKEY_Device_UINumberDescFormat


DEVPKEY_Device_UINumberDescFormat 设备属性表示一个**printf**兼容的格式字符串，该字符串应用于显示设备实例的 "DEVPKEY_DEVICE_UINumber 设备" 属性的值。

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
<td align="left"><p>DEVPKEY_Device_UINumberDescFormat</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的读取和写入访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>对应 SPDRP_</strong><em>Xxx</em> <strong>标识符</strong></p></td>
<td align="left"><p>SPDRP_UI_NUMBER_DESC_FORMAT</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

可以通过调用[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)来检索 DDEVPKEY_Device_UINumberDescFormat 的值，也可以通过调用[**SetupDiSetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)来设置此值。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_Device_UINumberDescFormat 属性键。 相反，你可以使用相应的 SPDRP_UI_NUMBER_DESC_FORMAT 标识符来访问这些早期版本的 Windows 上的属性值。 有关如何在这些早期版本的 Windows 上访问此属性值的信息，请参阅[SPDRP_Xxx 属性访问设备实例](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-instance-spdrp-xxx-properties)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows**头**： Devpkey （包括 Devpkey）


## <a name="see-also"></a>请参阅


[**INF AddReg 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)

[**INF DDInstall.HW 节**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-hw-section)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

[**SetupDiSetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)

 

 






