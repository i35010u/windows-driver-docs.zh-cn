---
title: DEVPKEY_DeviceClass_Exclusive
description: DEVPKEY_DeviceClass_Exclusive
ms.assetid: a05ada91-6a6f-4253-aca5-0740294a5c24
keywords:
- DEVPKEY_DeviceClass_Exclusive 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_Exclusive
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 64e28615bc6008a20130f1f28d9e8399e9df0fdb
ms.sourcegitcommit: e180a0670b0b78c30541755e6e030df249979f1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "86418542"
---
# <a name="devpkey_deviceclass_exclusive"></a>DEVPKEY_DeviceClass_Exclusive


DEVPKEY_DeviceClass_Exclusive 设备属性表示一个布尔型标志，该标志指示是[设备安装程序类](https://docs.microsoft.com/windows-hardware/drivers/install/device-setup-classes)的成员的设备是否为独占设备。

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
<td align="left"><p>DEVPKEY_DeviceClass_Exclusive</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-boolean.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_BOOLEAN&lt;/strong&gt;](devprop-type-boolean.md)"><strong>DEVPROP_TYPE_BOOLEAN</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序后，安装应用程序和安装程序的只读访问权限</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>对应 SPCRP_</strong><em>Xxx</em> <strong>标识符</strong></p></td>
<td align="left"><p>SPCRP_EXCLUSIVE</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

安装应用程序安装设备安装程序类时，可以设置 DEVPKEY_DeviceClass_Exclusive 的值。 有关如何安装设备安装程序类和设置此属性的信息，请参阅[**Inf ClassInstall32 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-classinstall32-section)和有关在[**inf AddReg 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)的 "特殊的*值-名称*关键字" 一节中**提供的注册表值的**信息。

可以调用[**SetupDiGetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)或[**SetupDiGetClassPropertyEx**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)来检索 DEVPKEY_DeviceClass_Exclusive 的值。

Windows Server 2003 和 Windows XP 支持此属性，但不支持 DEVPKEY_DeviceClass_Exclusive 属性键。 在这些早期版本的 Windows 中，可以使用 SPCRP_EXCLUSIVE 标识符来访问此属性的值。 有关如何访问此属性的值的信息，请参阅[检索设备安装程序类 SPCRP_Xxx 属性](https://docs.microsoft.com/windows-hardware/drivers/install/retrieving-spcrp-xxx-properties)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows**头**： Devpkey （包括 Devpkey）


## <a name="see-also"></a>请参阅


[**INF AddReg 指令**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-addreg-directive)

[**INF ClassInstall32 节**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-classinstall32-section)

[**SetupDiGetClassProperty**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyw)

[**SetupDiGetClassPropertyEx**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)

 

 






