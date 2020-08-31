---
title: INF AddProperty 指令
description: AddProperty 指令引用一个或多个 INF 文件节，这些节修改为设备实例、设备安装程序类、设备接口类或设备接口设置的设备属性。
ms.assetid: 8fcb1355-f13d-4d96-aa73-62a094a52267
keywords:
- INF AddProperty 指令设备和驱动程序安装
topic_type:
- apiref
api_name:
- INF AddProperty Directive
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e17d1f499643920c0753dd0c77a5e91758ed8f63
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096351"
---
# <a name="inf-addproperty-directive"></a>INF AddProperty 指令


**AddProperty**指令引用一个或多个 INF 文件节，这些节修改为设备实例、[设备安装程序类](./overview-of-device-setup-classes.md)、[设备接口类](./overview-of-device-interface-classes.md)或设备接口设置的[设备属性](device-properties.md)。

```inf
[DDInstall] |
[DDInstall.nt] |
[DDInstall.ntx86] |
[DDInstall.ntia64] |
[DDInstall.ntamd64] |
[DDInstall.ntarm] |
[DDInstall.ntarm64]
[ClassInstall32] | 
[ClassInstall32.nt] | 
[ClassInstall32.ntx86] |
[ClassInstall32.ntia64] |  (Windows XP and later versions of Windows)
[ClassInstall32.ntamd64]  |  (Windows XP and later versions of Windows)
[ClassInstall32.ntarm]  |  (Windows 8 and later versions of Windows)
[ClassInstall32.ntarm64]  |  (Windows 10 and later versions of Windows)
[interface-install-section] | 
[interface-install-section.nt] | 
[interface-install-section.ntx86] | 
[interface-install-section.ntia64] |  (Windows XP and later versions of Windows)
[interface-install-section.ntamd64]  (Windows XP and later versions of Windows) |
[interface-install-section.ntarm]  (Windows 8 and later versions of Windows) |
[interface-install-section.ntarm64]  (Windows 10 and later versions of Windows)
[add-interface-section]

AddProperty=add-property-section[,add-property-section]...  (Windows Vista and later versions of Windows)
...
```

每个 *添加属性部分* 都可以有项来执行以下操作：

-   添加设备属性并初始化属性的值。
-   修改现有设备属性的值。

**AddProperty**指令引用的*添加属性部分*具有以下格式：

```inf
[add-property-section]
(property-name, , , [flags], value]) | 
({property-category-guid}, property-pid, type, [flags], value)
...
```

Add 属性节可以有任意数量的 *属性名称* 条目或 *属性 guid* 条目，每个条目都在单独的行上。

## <a name="entries"></a>项


<a href="" id="property-name"></a>*属性-名称*  
以下属性名称之一，表示设备实例 [驱动程序包](driver-packages.md) 属性：

-   **DeviceModel**
-   **DeviceVendorWebsite**
-   **DeviceDetailedDescription**
-   **DeviceDocumentationLink**
-   **DeviceIcon**
-   **DeviceBrandingIcon**

有关添加自定义设备图标的详细信息，请参阅为 [设备提供图标](providing-vendor-icons-for-the-shell-and-autoplay.md)。

<a href="" id="property-category-guid"></a>*属性类别-guid*  
标识属性类别的 GUID 值。 GUID 值可以是系统定义的 GUID，用于标识设备实例、 [设备安装程序类](./overview-of-device-setup-classes.md)、 [设备接口类](./overview-of-device-interface-classes.md)或设备接口的属性类别之一。 具有相同 GUID 值的所有属性都是同一类别的成员。 这些属性类别是在 *Devpkey*中定义的。

GUID 值还可以是用于标识自定义属性类别的自定义 GUID 值。

<a href="" id="property-pid"></a>*属性-pid*  
属性标识符，指示属性类别中的特定属性，该属性由 *属性类别 guid* 值指示。 由于内部系统原因，属性标识符必须大于或等于2。

<a href="" id="type"></a>类别  
由属性-*类别 guid*值和*属性 pid*值指定的属性的[属性数据类型标识符](/previous-versions/ff541476(v=vs.85))的数字值（十进制或十六进制格式）。 仅支持以下 [**基本数据类型**](/previous-versions/ff537793(v=vs.85)) ：

-   DEVPROP_TYPE_STRING
-   DEVPROP_TYPE_STRING_LIST
-   DEVPROP_TYPE_BINARY
-   DEVPROP_TYPE_BOOLEAN
-   DEVPROP_TYPE_UINT32

例如，DEVPROP_TYPE_STRING 数据类型的十进制值为 18 (0x00000012) ，DEVPROP_TYPE_STRING_LIST 数据类型的十进制值为 2066 (0x00002012) 。

<a href="" id="flags"></a>*随意*  
可选的十六进制值，它是控制添加操作的以下标志的按位 OR。

<a href="" id="0x00000001--flg-addproperty-noclobber--"></a>**0x00000001** (FLG_ADDPROPERTY_NOCLOBBER)    
禁止值输入值替换现有属性值的标志。 如果驱动程序编写器希望使某个属性能够通过 **Include** 和 **需要** 指令进行重写，则编写器必须为该属性指定此标志。 这是因为当 Windows 处理包含和**需要****指令的 inf**部分内的所有其他指令后，windows 处理由**Include**和**需要**指令引用的 inf 部分。

<a href="" id="0x00000002--flg-addproperty-overwriteonly--"></a>**0x00000002** (FLG_ADDPROPERTY_OVERWRITEONLY)    
仅当指定的属性已存在时才将属性值设置为值输入值的标志。

<a href="" id="0x00000004--flg-addproperty-append--"></a>**0x00000004** (FLG_ADDPROPERTY_APPEND)    
将值输入值追加到现有属性字符串值的标志。 仅当属性数据类型为 DEVPROP_TYPE_STRING_LIST 时，此标志才有效。 如果所提供的字符串已存在于现有的字符串值中，则不会将提供的字符串追加到现有的属性字符串值。

<a href="" id="0x00000008--flg-addproperty-or-"></a>**0x00000008** (FLG_ADDPROPERTY_OR)   
一个标志，该标志对现有属性值的值输入值执行按位 "或" 运算。 仅当属性数据类型为 DEVPROP_TYPE_UINT32 时，此标志才有效。

<a href="" id="0x00000010--flg-addproperty-and-"></a>**0x00000010** (FLG_ADDPROPERTY_AND)   
一个标志，用于对现有属性值的值输入值执行按位 "与" 运算。 仅当属性数据类型为 DEVPROP_TYPE_UINT32 时，此标志才有效。

<a href="" id="value"></a>value  
添加操作用于修改属性值的值，具体取决于属性数据类型和 *标志* 项的值。

<a name="remarks"></a>备注
-------

**AddProperty**指令可用于修改系统定义的设备属性或自定义设备属性。 可以在上述正式语法语句中所示的任何部分中指定此指令。

在 INF 文件中，每个 *添加属性节* 名称必须是唯一的，但在同一 inf 文件中，可以由多个 **AddProperty** 指令引用部分。 每个节名称必须遵循用于定义 [用于 INF 文件一般语法规则](general-syntax-rules-for-inf-files.md)中所述的部分名称的常规规则。

有关如何使用 INF **AddProperty** 指令的详细信息，请参阅 [使用 inf ADDPROPERTY 指令和 inf DelProperty 指令](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)。

<a name="examples"></a>示例
--------

以下添加属性部分的示例包括两个行条目：第一个行条目按名称设置 **DeviceModel** 属性，第二行条目通过指定自定义属性密钥 GUID 设置自定义设备属性。

第一行包含 *属性名称* 条目值 "DeviceModel" 和 *值* 输入值 "采样设备型号名称"。

第二行条目在自定义属性类别中设置自定义属性。 属性类别 guid 条目值为 "c22189e4-8bf3-4e6d-8467-8dc6d95e2a7e"，属性标识符条目值为 "2"。

可选 *标志* 条目值不存在，并且类型条目值为 "18" (DEVPROP_TYPE_STRING) 。 值输入值为 "属性1的字符串值"。

```inf
[SampleAddPropertySection]
DeviceModel,,,,"Sample Device Model Name"
{c22189e4-8bf3-4e6d-8467-8dc6d95e2a7e}, 2, 18,, "String value for property 1"
```

## <a name="see-also"></a>另请参阅


[**DelProperty**](inf-delproperty-directive.md)

 

