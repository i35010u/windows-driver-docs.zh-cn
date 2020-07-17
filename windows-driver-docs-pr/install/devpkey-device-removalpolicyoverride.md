---
title: DEVPKEY_Device_RemovalPolicyOverride
description: DEVPKEY_Device_RemovalPolicyOverride
ms.assetid: 74b90422-9187-4bbb-9be6-cf2d11e29686
keywords:
- DEVPKEY_Device_RemovalPolicyOverride 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_Device_RemovalPolicyOverride
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5797bdbcfb8ff0594e2c7212437175a4d8e4d476
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418450"
---
# <a name="devpkey_device_removalpolicyoverride"></a>DEVPKEY_Device_RemovalPolicyOverride


DEVPKEY_Device_RemovalPolicyOverride 设备属性表示设备实例的删除策略覆盖。

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
<td align="left"><p>DEVPKEY_Device_RemovalPolicyOverride</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-int32.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_INT32&lt;/strong&gt;](devprop-type-int32.md)"><strong>DEVPROP_TYPE_INT32</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的读取和写入访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>对应 SPDRP_</strong><em>Xxx</em> <strong>标识符</strong></p></td>
<td align="left"><p>SPDRP_REMOVAL_POLICY_OVERRIDE</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

DEVPKEY_Device_RemovalPolicyOverride 的值是在 Cfgmgr32 中定义的 CM_REMOVAL_POLICY_*Xxx*值之一。

可以通过调用[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)来检索 DEVPKEY_Device_RemovalPolicyOverride 的值，也可以通过调用[**SetupDiSetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)来设置此值。

Windows Server 2003 和 Windows XP 支持此属性，但不支持 DEVPKEY_Device_RemovalPolicyOverride 属性键。 相反，你可以使用相应的 SPDRP_REMOVAL_POLICY_OVERRIDE 标识符来访问这些早期版本的 Windows 上的属性值。 有关如何在这些早期版本的 Windows 上访问此属性值的信息，请参阅[SPDRP_Xxx 属性访问设备实例](https://docs.microsoft.com/windows-hardware/drivers/install/accessing-device-instance-spdrp-xxx-properties)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows**头**： Devpkey （包括 Devpkey）


## <a name="see-also"></a>请参阅


[**SetupDiGetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)

[**SetupDiSetDeviceProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdisetdevicepropertyw)

 

 






