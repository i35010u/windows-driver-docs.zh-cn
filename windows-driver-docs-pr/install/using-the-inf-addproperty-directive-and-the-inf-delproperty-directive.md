---
title: 使用 INF AddProperty 指令和 INF DelProperty 指令
description: 使用 INF AddProperty 指令和 INF DelProperty 指令
ms.assetid: e5ae8d66-b2dc-409e-bdac-9034a9e24672
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cf63e5b2cb5d9ddda5d616d563f4f76fa07df949
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63339392"
---
# <a name="using-the-inf-addproperty-directive-and-the-inf-delproperty-directive"></a>使用 INF AddProperty 指令和 INF DelProperty 指令


在 Windows Vista 和更高版本的 Windows 中，可以使用[ **INF AddProperty 指令**](inf-addproperty-directive.md)并[ **INF DelProperty 指令**](inf-delproperty-directive.md)到设置和删除设备实例的属性[设备安装程序类](device-setup-classes.md)，[设备接口类](device-interface-classes.md)，和设备接口。 这包括[系统定义的设备属性](system-defined-device-properties2.md)并[自定义设备属性](creating-custom-device-properties.md)。 但是，应使用以下指导原则，当您使用**AddProperty**并**DelProperty**指令而不是[ **INF AddReg 指令**](inf-addreg-directive.md)并[ **INF DelReg 指令**](inf-delreg-directive.md)设置和删除设备属性：

-   有关引入 Windows Vista 和更高版本的 Windows 的设备属性，应使用**AddProperty**并**DelProperty**指令设置和删除设备属性。

-   在 Windows Server 2003、 Windows XP 或 Windows 2000 引入了，并且，可通过设置设备属性**AddReg**指令的和删除由**DelReg**指令，您应该继续使用**AddReg**并**DelReg**指令设置和删除这些设备属性。 不应使用**AddProperty**并**DelProperty**指令。

可以包括 INF **AddProperty**指令和 INF **DelProperty**指令后面的 INF 文件部分，设置并删除设备实例、 设备安装程序类、 设备属性接口类和设备接口：

-   [**INF DDInstall 部分**](inf-ddinstall-section.md)

-   [**INF ClassInstall32 部分**](inf-classinstall32-section.md)

-   *安装接口部分*引用[ **INF InterfaceInstall32 部分**](inf-interfaceinstall32-section.md)

-   *添加接口部分*引用[ **INF AddInterface 指令**](inf-addinterface-directive.md)

### <a name="using-the-inf-addproperty-directive"></a>使用 INF AddProperty 指令

若要修改的属性值，包括 INF **AddProperty**指令中安装的设备实例、 设备安装程序类、 设备接口类或设备接口的部分。 **AddProperty**指令引用一个或多个*添加属性节*包含指定属性的条目如何修改该属性，并且使用要修改的属性的值。 格式**AddProperty**指令是按如下所示：

**AddProperty=** <em>add-property-section</em>\[ **,** <em>add-property-section</em>\] ...

添加属性部分中的每行指定一个属性。 下图显示指定属性信息的两个可能的行格式。 显示的第一个行格式按名称指定的属性。 此格式可以仅可用于 DEVPKEY_DrvPkg_*Xxx*属性。 第二个行格式指定的属性类别和相应的属性标识符的属性[属性键](property-keys.md)。 此第二种格式可用于指定系统定义的属性或[自定义设备属性](creating-custom-device-properties.md)。

**\[** <em>添加属性部分</em> **\]** 
<em>属性名称</em> **、、、\[** <em>标志</em> ** \]，** <em>值</em>
 **{** <em>属性类别 guid</em> **}，** <em>属性 pid</em> **，** <em>类型</em> **，\[** <em>标志</em> ** \]，** <em>值</em>条目的值提供以下：

<a href="" id="property-name"></a>*property-name*  
名称标识 DEVPKEY_DrvPkg_*Xxx*属性。 例如， **DeviceModel**，表示[ **DEVPKEY_DrvPkg_Model** ](https://msdn.microsoft.com/library/windows/hardware/ff543523)属性，或者**DeviceVendorWebSite**，它表示[ **DEVPKEY_DrvPkg_VendorWebSite** ](https://msdn.microsoft.com/library/windows/hardware/ff543527)属性。

<a href="" id="property-category-guid"></a>*property-category-guid*  
属性所属的属性类别的 GUID 值。 例如，系统定义[ **DEVPKEY_Device_FriendlyName** ](https://msdn.microsoft.com/library/windows/hardware/ff542502)属性。 GUID 值还可以指定自定义设备类别。

<a href="" id="property-pid"></a>*property-pid*  
标识的属性类别中的属性的属性标识符。 例如，DEVPKEY_Device_FriendlyName 属性的属性标识符的值为 14。

<a href="" id="flags"></a>*标志*  
可选标志，指示如何修改属性值。

<a href="" id="type"></a>*Type*  
一个[属性数据类型标识符](property-data-type-identifiers.md)指定的数据类型。

<a href="" id="value"></a>*value*  
使用要修改的属性值的值。

下面的示例对**AddProperty**指令中包含了两个行项。 第一行包含*属性名称*条目值"DeviceModel"和*值*条目值，"示例设备模型名称"。 此项设置 DEVPKEY_DrvPkg_Model 属性。 第二行项设置自定义属性类别中的自定义属性。 *属性类别 guid*条目值是"c22189e4-8bf3-4e6d-8467-8dc6d95e2a7e"和*属性标识符*条目值是"2"。 可选*标志*条目值不存在并*类型*条目值为"18"(DEVPROP_TYPE_STRING)。 *值*条目值是"属性 1 为字符串值"。

```cpp
[Root_Install.NT]
AddProperty=Root_AddProperty

[Root_AddProperty]
DeviceModel,,,,"Sample Device Model Name"
{c22189e4-8bf3-4e6d-8467-8dc6d95e2a7e}, 2, 18,, "String value for property 1"
```

### <a name="using-the-inf-delproperty-directive"></a>使用 INF DelProperty 指令

若要删除的属性，包括 INF **DelProperty**指令中安装的设备实例、 设备安装程序类、 设备接口类或设备接口的部分。

主要目的[ **INF DelProperty 指令**](inf-delproperty-directive.md)供使用的 INF 文件中的设备安装更新。 在这种情况下， **DelProperty**指令可用于删除的设置是由以前的安装，但更新的安装不再需要的属性。 使用**DelProperty**指令谨慎使用。 **DelProperty**不应该用于删除系统组件或另一个 INF 文件可能还要设置的属性。

**DelProperty**指令具有以下格式：

**DelProperty=** <em>del-property-section</em>\[ **,** <em>del-property-section</em>\] ...

中的每一行*del 属性部分*指定一个属性。 下图显示指定属性信息的两个可能的行格式。 显示的第一个行格式按名称指定的属性。 此格式可以仅可用于 DEVPKEY_DrvPkg_*Xxx*属性。 第二个行格式指定的属性类别和相应的属性标识符的属性[属性键](property-keys.md)。 第二种格式可用于指定系统定义的属性或[自定义设备属性](creating-custom-device-properties.md)。

**\[** <em>del 属性部分</em> **\]** 
*属性名称* \[ **、** *标志* \[ **，** <em>值</em>\] \] **{** <em>属性类别 guid</em> **}，** *属性 pid* \[ **，** *标志* \[ **，** <em>值</em>\] \]条目的值提供以下：

<a href="" id="property-name"></a>*property-name*  
名称标识 DEVPKEY_DrvPkg_*Xxx*属性。 例如， **DeviceModel**，表示[ **DEVPKEY_DrvPkg_Model** ](https://msdn.microsoft.com/library/windows/hardware/ff543523)属性，或者**DeviceVendorWebSite**，它表示[ **DEVPKEY_Device_FriendlyName** ](https://msdn.microsoft.com/library/windows/hardware/ff542502)属性。

<a href="" id="property-category-guid"></a>*property-category-guid*  
属性所属的属性类别的 GUID 值。 例如，系统定义[ **DEVPKEY_Device_FriendlyName** ](https://msdn.microsoft.com/library/windows/hardware/ff542502)属性。 GUID 值还可以指定自定义设备类别。

<a href="" id="property-pid"></a>*property-pid*  
标识的属性类别中的属性的属性标识符。 例如，DEVPKEY_Device_FriendlyName 属性的属性标识符的值为 14。

<a href="" id="flags"></a>*标志*  
只能使用属性的数据类型是有效的可选标志[ **DEVPROP_TYPE_STRING_LIST**](https://msdn.microsoft.com/library/windows/hardware/ff543614)。 如果设置了标志，删除操作删除指定的字符串*值*从属性字符串列表。

<a href="" id="value"></a>*value*  
要从属性字符串列表中删除的字符串。

下面的示例对*del 属性部分*包括两个行项。

第一行包含*属性名称*条目值"DeviceModel"，删除 DEVPKEY_DrvPkg_Model 属性。 第二行项的数据类型是 DEVPROP_TYPE_STRING_LIST 的自定义设备属性值中删除"DeleteThisString"的字符串。 在第二个行中，*属性类别 guid*条目值是"c22189e4-8bf3-4e6d-8467-8dc6d95e2a7e"*属性标识符*条目值是"2"和*标志*条目值是"0x00000001。"

```cpp
[SampleDelPropertySection]
DeviceModel
{c22189e4-8bf3-4e6d-8467-8dc6d95e2a7e}, 2, 0x00000001, "DeleteThisString"
```

 

 





