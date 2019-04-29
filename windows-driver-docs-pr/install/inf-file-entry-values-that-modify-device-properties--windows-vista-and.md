---
title: 可修改设备属性的 INF 文件条目值
description: 可修改设备属性的 INF 文件条目值
ms.assetid: 5ce0875f-2687-42d9-b980-ed184b552a62
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4412180ff2ee00ed20e73490e409867b9eb15730
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379369"
---
# <a name="inf-file-entry-values-that-modify-device-properties"></a>可修改设备属性的 INF 文件条目值


修改 Windows Vista 及更高版本的设备属性的 INF 文件条目值如下：

-   INF 文件条目值集对应[系统定义的设备属性](system-defined-device-properties2.md)。

-   [**INF AddReg 指令**](inf-addreg-directive.md)并[ **INF DelReg 指令**](inf-delreg-directive.md)的设置或删除对应于系统定义的设备属性的系统定义的注册表条目值。

-   INF **AddReg**指令和 INF **DelReg**指令用于设置或删除自定义注册表项值

-   [**INF AddProperty 指令**](inf-addproperty-directive.md)并**INF DelProperty 指令**的设置和删除设备属性。 有关如何使用这些指令的详细信息，请参阅[INF AddProperty 指令和 INF DelProperty 指令](using-the-inf-addproperty-directive-and-the-inf-delproperty-directive.md)。

有关常规信息的 INF 文件安装设备实例的部分[设备安装程序类](device-setup-classes.md)，[设备接口类](device-interface-classes.md)，以及设备接口，请参阅以下主题：

[**INF *DDInstall*部分**](inf-ddinstall-section.md)

[**INF ClassInstall32 部分**](inf-classinstall32-section.md)

[**INF InterfaceInstall32 部分**](inf-interfaceinstall32-section.md)

[**INF *DDInstall*。接口部分**](inf-ddinstall-interfaces-section.md)

### <a href="" id="inf-file-entry-values-that-set-corresponding-system-defined-device-pro"></a>INF 文件条目值集相对应的系统定义的设备属性

某些 INF 文件条目的值提供 Windows 用来设置相应的系统定义的设备属性信息。 以下是几个示例的此类 INF 文件条目的值来提供值的设备属性：

-   [ **DEVPKEY_Device_DeviceDesc** ](https://msdn.microsoft.com/library/windows/hardware/ff542407)设备实例属性设置*设备描述*中的项值[ **INF模型部分**](inf-models-section.md)。

-   [ **DEVPKEY_DeviceClass_ClassName** ](https://msdn.microsoft.com/library/windows/hardware/ff542272)属性[设备安装程序类](device-setup-classes.md)通过设置*类名*INF中的项值**类**指令[ **INF 版本部分**](inf-version-section.md)。

-   [ **DEVPKEY_DeviceInterface_ClassGuid** ](https://msdn.microsoft.com/library/windows/hardware/ff542349)设备接口的属性设置*InterfaceClassGuid*中的项值[ **INF InterfaceInstall32 部分**](inf-interfaceinstall32-section.md)。

### <a href="" id="inf-addreg-directives-and-inf-delreg-directives-that-modify-system-def"></a>INF AddReg 指令和修改系统定义的设备属性的 INF DelReg 指令

许多系统定义的设备属性有对应的系统定义的注册表项值。 具有对应的注册表条目的设备属性的值，使用[ **INF AddReg 指令**](inf-addreg-directive.md)添加相应的注册表项值设置相应的设备属性。 同样，使用[ **INF DelReg 指令**](inf-delreg-directive.md)删除注册表条目值，将删除相应的设备属性。

例如，以下**AddReg**指令将设置**DeviceCharacteristics**注册表条目值，以及设备的相应的 DEVPKEY_Device_Characteristics 属性实例的数据类型安装由"Abc_Device_Install.HW"部分。

```ini
[Abc_Device_Install.HW]
...
AddReg = Xxx_AddReg
...
[Xxx_AddReg]
...
[HKR,,DeviceCharacteristics,0x10001,0x00000001
] 
```

### <a href="" id="inf-addreg-directives-and-inf-delreg-directives-that-modify-custom-reg"></a>INF AddReg 指令和修改自定义注册表项值的 INF DelReg 指令

Windows Vista 和更高版本支持使用[ **INF AddReg 指令**](inf-addreg-directive.md)并[ **INF DelReg 指令**](inf-delreg-directive.md)来修改自定义注册表条目表示自定义设备属性的值。 但是，自定义注册表条目的值来表示设备属性不支持创建统一的设备属性模型。 如果您创建的设备的自定义注册表条目值，必须以相同方式管理注册表条目值，管理 Windows Server 2003、 Windows XP 和 Windows 2000 上如此。 若要简化自定义设备属性管理，应创建设备属性键来呈现自定义设备属性，而不是创建自定义注册表条目的值。









