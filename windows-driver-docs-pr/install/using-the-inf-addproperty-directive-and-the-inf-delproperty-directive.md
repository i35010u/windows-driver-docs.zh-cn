---
title: 使用 INF AddProperty 指令和 INF DelProperty 指令
description: 使用 INF AddProperty 指令和 INF DelProperty 指令
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c714c9ed1ee6c38359706cf1b3bfe46de0c31801
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96840961"
---
# <a name="using-the-inf-addproperty-directive-and-the-inf-delproperty-directive"></a>使用 INF AddProperty 指令和 INF DelProperty 指令


在 Windows Vista 和更高版本的 Windows 中，可以使用 [**Inf AddProperty 指令**](inf-addproperty-directive.md) 和 [**inf DelProperty 指令**](inf-delproperty-directive.md) 来设置和删除设备实例、 [设备安装程序类](./overview-of-device-setup-classes.md)、 [设备接口类](./overview-of-device-interface-classes.md)和设备接口的属性。 这包括 [系统定义的设备属性](system-defined-device-properties2.md) 和 [自定义设备属性](creating-custom-device-properties.md)。 但是，在使用 **AddProperty** 和 **DelProperty** 指令而不是 [**Inf AddReg 指令**](inf-addreg-directive.md) 和 [**inf DelReg 指令**](inf-delreg-directive.md) 来设置和删除设备属性时，应使用以下准则：

-   对于 Windows Vista 和更高版本的 Windows 上引入的设备属性，你应使用 **AddProperty** 和 **DelProperty** 指令来设置和删除设备属性。

-   对于 Windows Server 2003、Windows XP 或 Windows 2000 上引入的设备属性，以及可由 **AddReg** 指令设置并由 **DelReg** 指令删除的设备属性，应继续使用 **AddReg** 和 **DelReg** 指令来设置和删除这些设备属性。 不应使用 **AddProperty** 和 **DelProperty** 指令。

可以在以下 INF 文件部分中包括 INF **AddProperty** 指令和 inf **DelProperty** 指令，以设置和删除设备实例、设备安装程序类、设备接口类和设备接口的属性：

-   [**INF DDInstall 节**](inf-ddinstall-section.md)

-   [**INF ClassInstall32 节**](inf-classinstall32-section.md)

-   [**INF InterfaceInstall32 部分**](inf-interfaceinstall32-section.md)引用的 *安装界面部分*

-   由 [**INF AddInterface 指令**](inf-addinterface-directive.md)引用的 *添加接口部分*

### <a name="using-the-inf-addproperty-directive"></a>使用 INF AddProperty 指令

若要修改属性值，请在安装设备实例、设备安装程序类、设备接口类或设备接口的部分中包括 INF **AddProperty** 指令。 **AddProperty** 指令引用一个或多个 *添加属性节*，其中包含指定属性的项、如何修改属性以及用于修改属性的值。 **AddProperty** 指令的格式如下所示：

**AddProperty =**<em>添加属性</em>-节 \[ **，**<em>添加属性-节</em> \] .。。

添加属性部分中的每行指定一个属性。 下面显示了两个可能的行格式，它们指定属性信息。 显示的第一行格式按其名称指定属性。 此格式只能与 DEVPKEY_DrvPkg_ *Xxx* 属性一起使用。 第二个线条格式通过相应 [属性键](property-keys.md)的属性类别和属性标识符来指定属性。 此第二种格式可用于指定系统定义的属性或 [自定义设备属性](creating-custom-device-properties.md)。

**\[**<em>添加-属性部分</em> **\]** 
<em>属性-名称</em>**,,, \[**<em>标志</em>**\] 、**<em>值</em> 
 **{**<em>属性类别-guid</em>**}、**<em>属性 pid</em>**、**<em>类型</em>**、 \[**<em>标志</em>**\] 、**<em>值</em>输入值提供以下内容：

<a href="" id="property-name"></a>*属性-名称*  
标识 DEVPKEY_DrvPkg_ *Xxx* 属性的名称。 例如， **DeviceModel** 表示 [**DEVPKEY_DrvPkg_VendorWebSite**](./devpkey-drvpkg-vendorwebsite.md)属性的 [**DEVPKEY_DrvPkg_Model**](./devpkey-drvpkg-model.md)属性或 **DeviceVendorWebSite**。

<a href="" id="property-category-guid"></a>*属性类别-guid*  
属性所属的属性类别的 GUID 值。 例如，系统定义的 [**DEVPKEY_Device_FriendlyName**](./devpkey-device-friendlyname.md) 属性。 GUID 值还可以指定自定义设备类别。

<a href="" id="property-pid"></a>*属性-pid*  
标识属性类别中属性的属性标识符。 例如，DEVPKEY_Device_FriendlyName 属性的属性标识符的值为14。

<a href="" id="flags"></a>*随意*  
指示如何修改属性值的可选标志。

<a href="" id="type"></a>*类别*  
指定数据类型的 [属性数据类型标识符](property-data-type-identifiers.md) 。

<a href="" id="value"></a>value  
用于修改属性值的值。

下面的 **AddProperty** 指令示例包含两个行条目。 第一行包含 *属性名称* 条目值 "DeviceModel" 和 *值* 输入值 "采样设备型号名称"。 此项设置 DEVPKEY_DrvPkg_Model 属性。 第二行条目在自定义属性类别中设置自定义属性。 *属性类别 guid* 条目值为 "c22189e4-8bf3-4e6d-8467-8dc6d95e2a7e"，*属性标识符* 条目值为 "2"。 可选的 *Flags* 条目值不存在， *类型* entry 值为 "18" (DEVPROP_TYPE_STRING) 。 *值* 输入值为 "属性1的字符串值"。

```cpp
[Root_Install.NT]
AddProperty=Root_AddProperty

[Root_AddProperty]
DeviceModel,,,,"Sample Device Model Name"
{c22189e4-8bf3-4e6d-8467-8dc6d95e2a7e}, 2, 18,, "String value for property 1"
```

### <a name="using-the-inf-delproperty-directive"></a>使用 INF DelProperty 指令

若要删除属性，请在安装设备实例、设备安装程序类、设备接口类或设备接口的部分中包括 INF **DelProperty** 指令。

[**Inf DelProperty 指令**](inf-delproperty-directive.md)的主要用途是在用于更新设备安装的 inf 文件中使用。 在这种情况下， **DelProperty** 指令可用于删除以前安装设置的属性，但更新的安装不再需要该属性。 使用 **DelProperty** 指令时要格外小心。 不应使用 **DelProperty** 来删除可能还由系统组件或其他 INF 文件设置的属性。

**DelProperty** 指令具有以下格式：

**DelProperty =**<em>del-property 节</em> \[ **，**<em>del</em> \] .。。

*Del-属性部分* 中的每行指定一个属性。 下面显示了两个可能的行格式，它们指定属性信息。 显示的第一行格式按其名称指定属性。 此格式只能与 DEVPKEY_DrvPkg_ *Xxx* 属性一起使用。 第二个线条格式通过相应 [属性键](property-keys.md)的属性类别和属性标识符来指定属性。 第二种格式可用于指定系统定义的属性或 [自定义设备属性](creating-custom-device-properties.md)。

**\[**<em>del-属性部分</em> **\]** 
*属性-名称* \[**，，** *标志* \[ **，**<em>值</em> \] \] **{**<em>属性类别-guid</em>**}，** *属性 pid* \[ **，** *标志* \[ **，**<em>值</em> \] \] 输入值提供以下内容：

<a href="" id="property-name"></a>*属性-名称*  
标识 DEVPKEY_DrvPkg_ *Xxx* 属性的名称。 例如， **DeviceModel** 表示 [**DEVPKEY_Device_FriendlyName**](./devpkey-device-friendlyname.md)属性的 [**DEVPKEY_DrvPkg_Model**](./devpkey-drvpkg-model.md)属性或 **DeviceVendorWebSite**。

<a href="" id="property-category-guid"></a>*属性类别-guid*  
属性所属的属性类别的 GUID 值。 例如，系统定义的 [**DEVPKEY_Device_FriendlyName**](./devpkey-device-friendlyname.md) 属性。 GUID 值还可以指定自定义设备类别。

<a href="" id="property-pid"></a>*属性-pid*  
标识属性类别中属性的属性标识符。 例如，DEVPKEY_Device_FriendlyName 属性的属性标识符的值为14。

<a href="" id="flags"></a>*随意*  
仅适用于其数据类型为 [**DEVPROP_TYPE_STRING_LIST**](./devprop-type-string-list.md)的属性的可选标志。 如果设置了标志，则删除操作将从属性字符串列表中删除通过 *值* 指定的字符串。

<a href="" id="value"></a>value  
要从属性字符串列表中删除的字符串。

下面的一个 *del 属性部分* 示例包含两个行条目。

第一行包含 *属性名称* 条目值 "DeviceModel"，它将删除 DEVPKEY_DrvPkg_Model 属性。 第二行条目从 DEVPROP_TYPE_STRING_LIST 的数据类型的自定义设备属性值中删除字符串 "DeleteThisString"。 在第二行中， *属性-category-guid* 条目值为 "c22189e4-8bf3-4e6d-8467-8dc6d95e2a7e"， *属性标识符* 条目值为 "2"， *标志* 条目值为 "0x00000001"。

```cpp
[SampleDelPropertySection]
DeviceModel
{c22189e4-8bf3-4e6d-8467-8dc6d95e2a7e}, 2, 0x00000001, "DeleteThisString"
```

 

