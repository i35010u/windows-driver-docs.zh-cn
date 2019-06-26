---
title: DEVPKEY_Device_UINumber
description: DEVPKEY_Device_UINumber
ms.assetid: 81bd0b71-909d-49c3-8d6c-258c57f80644
keywords:
- DEVPKEY_Device_UINumber 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_UINumber
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: bd278c42e9c7e4e7212e0295644201ef74ba9c29
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67363006"
---
# <a name="devpkeydeviceuinumber"></a>DEVPKEY_Device_UINumber


DEVPKEY_Device_UINumber 设备属性表示为设备实例可以在用户界面项中显示的数字。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_Device_UINumber</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-int32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_INT32&lt;/strong&gt;](devprop-type-int32.md)"><strong>DEVPROP_TYPE_INT32</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>属性访问</strong></p></td>
<td align="left"><p>通过安装应用程序和安装程序的只读访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>相应 SPDRP_</strong><em>Xxx</em> <strong>标识符</strong></p></td>
<td align="left"><p>SPDRP_UI_NUMBER</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>本地化？</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

Windows 为 UINumber 成员的值设置的值 DEVPKEY_Device_UINumber [ **DEVICE_CAPABILITIES** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)设备实例结构。 设备实例总线驱动程序返回此值以响应[ **IRP_MN_QUERY_CAPABILITIES** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)请求。

您可以调用[ **SetupDiGetDeviceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)检索 DEVPKEY_Device_UINumber 值。

Windows Server 2003、 Windows XP 和 Windows 2000 支持此属性，但不是支持 DEVPKEY_Device_UINumber 属性键。 相反，相应的 SPDRP_UI_NUMBER 标识符可用于访问这些早期版本的 Windows 上的属性的值。 有关如何访问这些早期版本的 Windows 上此属性的值的信息，请参阅[访问设备实例 SPDRP_Xxx 属性](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-instance-spdrp-xxx-properties)。

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


[**DEVICE_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/ns-wdm-_device_capabilities)

[**IRP_MN_QUERY_CAPABILITIES**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-capabilities)

[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

 

 






