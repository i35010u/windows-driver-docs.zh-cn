---
title: INF AddProperty 指令
description: AddProperty 指令引用修改为设备实例、 设备安装程序类、 设备接口类或设备接口设置的设备属性的一个或多个 INF 文件部分。
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
ms.openlocfilehash: 3af574a8deeac086922eca11a811b8e717d1ca7d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56540603"
---
# <a name="inf-addproperty-directive"></a>INF AddProperty 指令


**AddProperty**指令引用一个或多个修改的 INF 文件节[设备属性](device-properties.md)设备实例，设置[设备安装程序类](device-setup-classes.md)， [设备接口类](device-interface-classes.md)，或设备接口。

```ini
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

每个*添加属性部分*可以有条目以执行以下操作：

-   添加的设备属性和初始化属性的值。
-   修改现有的设备属性的值。

*添加属性部分*引用**AddProperty**指令具有以下格式：

```ini
[add-property-section]
(property-name, , , [flags], value]) | 
({property-category-guid}, property-pid, type, [flags], value)
...
```

添加属性部分可以具有任意数量的*属性名称*条目或*属性 guid*条目，每个单独的行上。

## <a name="entries"></a>条目


<a href="" id="property-name"></a>*property-name*  
以下属性之一的设备实例名称，分别代表[驱动程序包](driver-packages.md)属性：

-   **DeviceModel**
-   **DeviceVendorWebsite**
-   **DeviceDetailedDescription**
-   **DeviceDocumentationLink**
-   **DeviceIcon**
-   **DeviceBrandingIcon**

<a href="" id="property-category-guid"></a>*property-category-guid*  
一个 GUID 值，该值标识属性类别。 GUID 值可以是一个系统定义的 GUID，用于标识设备实例，将属性类别之一[设备安装程序类](device-setup-classes.md)即[设备接口类](device-interface-classes.md)，或设备接口。 具有相同的 GUID 值的所有属性都都为相同类别的成员。 这些属性类别中定义*Devpkey.h*。

GUID 值也可以是自定义的 GUID 值标识的自定义属性类别。

<a href="" id="property-pid"></a>*property-pid*  
指示所指示的属性类别中的特定属性的属性标识符*属性类别 guid*值。 内部系统方面的考虑，属性标识符必须大于或等于 2。

<a href="" id="type"></a>type  
中的数值，十进制或十六进制格式的[属性数据类型标识符](https://msdn.microsoft.com/library/windows/hardware/ff541476)由指定的属性*属性类别 guid*值和*属性 pid*值。 仅以下[**基本数据类型**](https://msdn.microsoft.com/library/windows/hardware/ff537793)支持：

-   DEVPROP_TYPE_STRING
-   DEVPROP_TYPE_STRING_LIST
-   DEVPROP_TYPE_BINARY
-   DEVPROP_TYPE_BOOLEAN
-   DEVPROP_TYPE_UINT32

例如，DEVPROP_TYPE_STRING 数据类型的十进制值为 18 (0x00000012) 和 DEVPROP_TYPE_STRING_LIST 数据类型的十进制值是 2066 (0x00002012)。

<a href="" id="flags"></a>*flags*  
可选的十六进制值，它是控制添加操作的以下标志的按位 OR:

<a href="" id="0x00000001--flg-addproperty-noclobber--"></a>**0x00000001** (FLG_ADDPROPERTY_NOCLOBBER)   
一个标志，可防止值条目值替换现有的属性值。 如果驱动程序编写者想要使属性能够通过重写**Include**并**需要**指令，编写器必须指定该属性的此标志。 这是因为 Windows 处理由引用的 INF 部分**Include**并**需要**指令后 Windows 处理包含INF部分中的所有其他指令**Include**并**需要**指令。

<a href="" id="0x00000002--flg-addproperty-overwriteonly--"></a>**0x00000002** (FLG_ADDPROPERTY_OVERWRITEONLY)   
一个标志，将属性值设置为值条目值，仅当指定的属性已存在。

<a href="" id="0x00000004--flg-addproperty-append--"></a>**0x00000004** (FLG_ADDPROPERTY_APPEND)   
一个标志，用于将值项值追加到的现有属性的字符串值。 此标志为属性数据类型是 DEVPROP_TYPE_STRING_LIST 才有效。 如果所提供的字符串中已存在现有的字符串值，所提供的字符串不被追加到现有的属性字符串值。

<a href="" id="0x00000008--flg-addproperty-or-"></a>**0x00000008** (FLG_ADDPROPERTY_OR)  
一个标志，执行位或运算的值与现有属性值的值项值。 此标志为属性数据类型是 DEVPROP_TYPE_UINT32 才有效。

<a href="" id="0x00000010--flg-addproperty-and-"></a>**0x00000010** (FLG_ADDPROPERTY_AND)  
一个标志，执行按位与的值与现有属性值的值项值。 此标志为属性数据类型是 DEVPROP_TYPE_UINT32 才有效。

<a href="" id="value"></a>*value*  
添加操作用来修改属性值，具体取决于属性数据类型和值的值*标志*条目。

<a name="remarks"></a>备注
-------

**AddProperty**指令可用于修改系统定义的设备属性或自定义设备属性。 任何正式语法语句更高版本中所示的部分下，可以指定此指令。

每个*添加属性部分*名称中必须是唯一的 INF 文件，但部分可以被多个**AddProperty**指令相同的 INF 文件中。 每个节名必须遵循的一般规则用于定义中所述的节名称[INF 文件的常规语法规则](general-syntax-rules-for-inf-files.md)。

详细了解如何使用 INF **AddProperty**指令，请参阅[INF AddProperty 指令和 INF DelProperty 指令](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)。

<a name="examples"></a>示例
--------

属性部分，添加下面的示例包含两个行项： 第一个行条目集**DeviceModel**属性按名称和第二个行条目通过指定自定义属性键 GUID 来设置自定义设备属性。

第一行包含*属性名称*条目值"DeviceModel"和*值*条目值，"示例设备模型名称"。

第二行项设置自定义属性类别中的自定义属性。 属性类别 guid 项值为"c22189e4-8bf3-4e6d-8467-8dc6d95e2a7e"，属性标识符条目值为"2"。

可选*标志*条目值不存在，并且类型条目值为"18"(DEVPROP_TYPE_STRING)。 将值项值是"属性 1 为字符串值"。

```ini
[SampleAddPropertySection]
DeviceModel,,,,"Sample Device Model Name"
{c22189e4-8bf3-4e6d-8467-8dc6d95e2a7e}, 2, 18,, "String value for property 1"
```

## <a name="see-also"></a>另请参阅


[**DelProperty**](inf-delproperty-directive.md)

 

 






