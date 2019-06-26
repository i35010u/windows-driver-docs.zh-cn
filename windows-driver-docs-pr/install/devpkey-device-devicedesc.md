---
title: DEVPKEY_Device_DeviceDesc
description: DEVPKEY_Device_DeviceDesc
ms.assetid: 02b88ee7-d825-48d9-99ef-aac8e6748141
keywords:
- DEVPKEY_Device_DeviceDesc 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_DeviceDesc
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b3e8a496c5fe47909ce8e225d34522433e3ea069
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387082"
---
# <a name="devpkeydevicedevicedesc"></a>DEVPKEY_Device_DeviceDesc


DEVPKEY_Device_DeviceDesc 设备属性表示设备实例的说明。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_DeviceDesc</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>通过安装应用程序和安装程序的只读访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>相应 SPDRP_</strong><em>Xxx</em> <strong>标识符</strong></p></td>
<td align="left"><p>SPDRP_DEVICEDESC</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>是</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

DEVPKEY_Device_DeviceDesc 的值将由*设备描述*由提供的项值[ **INF 模型部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-models-section)的安装的 INF 文件设备。

您可以调用[ **SetupDiGetDeviceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)检索 DEVPKEY_DEVICE_DeviceDesc 值。

可以检索的值[ **DEVPKEY_NAME** ](devpkey-name--device-instance-.md)要检索的设备的名称应显示在用户界面项中的设备实例属性。

Windows Server 2003、 Windows XP 和 Windows 2000 支持此属性，但不是支持 DEVPKEY_Device_DeviceDesc 属性键。 相反，这些早期版本的 Windows 使用的相应 SPDRP_DEVICEDESC 标识符访问属性的值。 有关如何访问这些早期版本的 Windows 上此属性的值的信息，请参阅[访问设备实例 SPDRP_Xxx 属性](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-instance-spdrp-xxx-properties)。

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
<td align="left">Devpkey.h （包括 Devpkey.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**DEVPKEY_NAME （设备实例）** ](devpkey-name--device-instance-.md)

[**INF 模型部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-models-section)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






