---
title: DEVPKEY_DeviceClass_DefaultService
description: DEVPKEY_DeviceClass_DefaultService
ms.assetid: 19d1a9ea-3bde-4230-af1a-b67b5a29e6f4
keywords:
- DEVPKEY_DeviceClass_DefaultService 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DEVPKEY_DeviceClass_DefaultService
api_location:
- Devpkey.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 49e7101b89fc8072401cf45acfd43f212e5dc915
ms.sourcegitcommit: b84d760d4b45795be12e625db1d5a4167dc2c9ee
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/17/2020
ms.locfileid: "90715776"
---
# <a name="devpkey_deviceclass_defaultservice"></a>DEVPKEY_DeviceClass_DefaultService


DEVPKEY_DeviceClass_DefaultService 设备属性表示 [设备安装程序类](./overview-of-device-setup-classes.md)的默认服务的名称。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr>
<th>Attribute</th>
<th>值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>属性键</strong></p></td>
<td align="left"><p>DEVPKEY_DeviceClass_DefaultService</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>属性数据类型标识符</strong></p></td>
<td align="left"><p><a href="devprop-type-string.md" data-raw-source="[&lt;strong&gt;DEVPROP_TYPE_STRING&lt;/strong&gt;](devprop-type-string.md)"><strong>DEVPROP_TYPE_STRING</strong></a></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>和</strong></p></td>
<td align="left"><p>安装应用程序和安装程序的只读访问</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>对应的注册表值名称</strong></p></td>
<td align="left"><p><strong>默认服务</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>各种?</strong></p></td>
<td align="left"><p>否</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

如果为设备安装程序类安装了默认服务，且设备未安装特定于设备的服务，则安装该类的 INF 文件的 [**Inf ClassInstall32 部分**](./inf-classinstall32-services-section.md) 会为设备安装类默认服务。

DEVPKEY_DeviceClass_DefaultService 的值是类注册表项下的 **默认服务** 注册表值的值。

可以调用 [**SetupDiGetClassProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertyw) 或 [**SetupDiGetClassPropertyEx**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertyexw) 来检索 DEVPKEY_DeviceClass_DefaultService 的值。

Windows Server 2003、Windows XP 和 Windows 2000 支持此属性，但不支持 DEVPKEY_DeviceClass_DefaultService 属性键。 您可以通过访问类注册表项下的相应 **默认服务** 注册表值访问此属性的值。 有关如何访问类注册表项下的值项的信息，请参阅 [访问类注册表项下的注册表项值](./accessing-registry-entry-values-under-the-class-registry-key.md)。

<a name="requirements"></a>要求
------------

**版本**： windows Vista 和更高版本的 windows **标题**： Devpkey (包含 Devpkey) 


## <a name="see-also"></a>请参阅


[**INF ClassInstall32.Services 节**](./inf-classinstall32-services-section.md)

[**SetupDiGetClassProperty**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertyw)

[**SetupDiGetClassPropertyEx**](/windows/win32/api/setupapi/nf-setupapi-setupdigetclasspropertyexw)

 

