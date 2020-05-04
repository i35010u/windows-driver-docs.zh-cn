---
title: 可修改设备属性的 INF 文件条目值
description: 可修改设备属性的 INF 文件条目值
ms.assetid: 5ce0875f-2687-42d9-b980-ed184b552a62
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e1e559695ecaa71a3924d620c5f05600527571eb
ms.sourcegitcommit: a55489992dbf0a7e9d09f237e13514799711647a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "82223159"
---
# <a name="inf-file-entry-values-that-modify-device-properties"></a>可修改设备属性的 INF 文件条目值


以下是在 Windows Vista 和更高版本上修改设备属性的 INF 文件条目值：

-   INF 文件输入值，用于设置相应的[系统定义的设备属性](system-defined-device-properties2.md)。

-   [**Inf AddReg 指令**](inf-addreg-directive.md)和[**inf DelReg 指令**](inf-delreg-directive.md)，用于设置或删除系统定义的注册表项值，这些值与系统定义的设备属性相对应。

-   INF **AddReg**指令和 inf **DelReg**指令，用于设置或删除自定义注册表项值

-   用于设置和删除设备属性的[**Inf AddProperty 指令**](inf-addproperty-directive.md)和**inf DelProperty 指令**。 有关如何使用这些指令的详细信息，请参阅[使用 Inf AddProperty 指令和 Inf DelProperty 指令](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)。

有关安装设备实例、[设备安装程序类](device-setup-classes.md)、[设备接口类](device-interface-classes.md)和设备接口的 INF 文件部分的常规信息，请参阅以下主题：

[**INF *DDInstall*部分**](inf-ddinstall-section.md)

[**INF ClassInstall32 节**](inf-classinstall32-section.md)

[**INF InterfaceInstall32 节**](inf-interfaceinstall32-section.md)

[**INF *DDInstall*。接口部分**](inf-ddinstall-interfaces-section.md)

### <a name="inf-file-entry-values-that-set-corresponding-system-defined-device-properties"></a><a href="" id="inf-file-entry-values-that-set-corresponding-system-defined-device-pro"></a>用于设置相应系统定义设备属性的 INF 文件输入值

某些 INF 文件输入值提供 Windows 用于设置相应系统定义的设备属性的信息。 下面是一些设备属性示例，它们的值由以下 INF 文件条目值提供：

-   设备实例的[**DEVPKEY_Device_DeviceDesc**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-device-devicedesc)属性是通过 " [**INF 模型" 部分**](inf-models-section.md)中的*设备说明*条目值设置的。

-   [设备安装程序类](device-setup-classes.md)的[**DEVPKEY_DeviceClass_ClassName**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-deviceclass-classname)属性是由[**INF 版本部分**](inf-version-section.md)中的 inf**类**指令中的*类名称*条目值设置的。

-   设备接口的[**DEVPKEY_DeviceInterface_ClassGuid**](https://docs.microsoft.com/windows-hardware/drivers/install/devpkey-deviceinterface-classguid)属性是由[**INF InterfaceInstall32 部分**](inf-interfaceinstall32-section.md)中的*InterfaceClassGuid*条目值设置的。

### <a name="inf-addreg-directives-and-inf-delreg-directives-that-modify-system-defined-device-properties"></a><a href="" id="inf-addreg-directives-and-inf-delreg-directives-that-modify-system-def"></a>用于修改系统定义的设备属性的 INF AddReg 指令和 INF DelReg 指令

许多系统定义的设备属性具有相应的系统定义的注册表项值。 对于具有相应注册表项值的设备属性，使用[**INF AddReg 指令**](inf-addreg-directive.md)添加相应的注册表项值将设置相应的设备属性。 同样，使用[**INF DelReg 指令**](inf-delreg-directive.md)删除注册表项值时，将删除相应的设备属性。

例如，以下**AddReg**指令将设置由 "Abc_Device_Install HW" 部分安装的设备实例的**DeviceCharacteristics**注册表项值和相应的 DEVPKEY_Device_Characteristics 属性。

```inf
[Abc_Device_Install.HW]
...
AddReg = Xxx_AddReg
...
[Xxx_AddReg]
...
[HKR,,DeviceCharacteristics,0x10001,0x00000001
] 
```

### <a name="inf-addreg-directives-and-inf-delreg-directives-that-modify-custom-registry-entry-values"></a><a href="" id="inf-addreg-directives-and-inf-delreg-directives-that-modify-custom-reg"></a>用于修改自定义注册表项值的 INF AddReg 指令和 INF DelReg 指令

Windows Vista 和更高版本支持使用[**Inf AddReg 指令**](inf-addreg-directive.md)和[**inf DelReg 指令**](inf-delreg-directive.md)来修改表示自定义设备属性的自定义注册表项值。 但是，统一设备属性模型不支持创建自定义注册表项值来表示设备属性。 如果为设备创建自定义注册表项值，则必须以在 Windows Server 2003、Windows XP 和 Windows 2000 上管理注册表项值的相同方式管理这些注册表项值。 为了简化自定义设备属性的管理，你应创建设备属性键来表示自定义设备属性，而不是创建自定义注册表项值。









