---
title: INF 文件条目的值修改 Windows Vista 之前的设备属性
description: INF 文件条目的值修改 Windows Vista 之前的设备属性
ms.assetid: b2a1f265-fc9b-47fb-83af-b4f66d79da83
keywords:
- 设备属性 WDK 设备安装，修改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 162ef532419035b1434bce610760afd25745122f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542897"
---
# <a name="inf-file-entry-values-that-modify-device-properties-before-windows-vista"></a>INF 文件条目的值修改 Windows Vista 之前的设备属性


修改 Windows Server 2003、 Windows XP 和 Windows 2000 上的设备属性的 INF 文件条目值如下：

-   设置设备属性的 INF 文件条目值对应于[系统定义的设备属性](https://msdn.microsoft.com/library/windows/hardware/ff553413)属于[统一的设备属性模型](unified-device-property-model--windows-vista-and-later-.md)在 Windows Vista 和更高版本的Windows。

-   [**INF AddReg 指令**](inf-addreg-directive.md)并[ **INF DelReg 指令**](inf-delreg-directive.md)的设置或删除对应的系统定义的设备属性的系统定义的注册表项值是 Windows Vista 和更高版本中的统一的设备属性模型的一部分。

-   INF **AddReg**指令和 INF **DelReg**指令用于设置或删除自定义注册表条目对应于自定义设备属性的值。

有关常规信息的 INF 文件安装设备实例的部分[设备安装程序类](device-setup-classes.md)，[设备接口类](device-interface-classes.md)，以及设备接口，请参阅以下主题：

[**INF *DDInstall*部分**](inf-ddinstall-section.md)

[**INF ClassInstall32 部分**](inf-classinstall32-section.md)

[**INF InterfaceInstall32 部分**](inf-interfaceinstall32-section.md)

[**INF *DDInstall*。接口部分**](inf-ddinstall-interfaces-section.md)

### <a href="" id="inf-file-entry-values-that-correspond-to-system-defined-device-propert"></a>INF 文件条目对应于系统定义的设备属性的值

某些 INF 文件条目的值提供 Windows 用来设置为设备实例属性和设备接口属性的系统定义的注册表条目的值相对应的信息。 以下是几个示例提供的此类 INF 文件条目的值的注册表项值：

-   [ **INF 模型部分**](inf-models-section.md)的 INF 文件包含*设备描述*条目值。 此值对应于[ **DEVPKEY_Device_DeviceDesc** ](https://msdn.microsoft.com/library/windows/hardware/ff542407)统一的设备属性中属性的模型，并且可以通过调用检索[ **SetupDiGetDeviceRegistryProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551967)并设置*属性*SPDRP_DEVICEDESC 参数。

-   INF**类**指令[ **INF 版本部分**](inf-version-section.md)包括*类名*条目值，用于提供的名称[设备安装程序类](device-setup-classes.md)。 此值对应于[ **DEVPKEY_DeviceClass_ClassName** ](https://msdn.microsoft.com/library/windows/hardware/ff542272)统一的设备属性模型中的属性。 可以通过调用来检索设备安装程序类的类名[ **SetupDiClassNameFromGuid**](https://msdn.microsoft.com/library/windows/hardware/ff550947)，并且可以通过调用检索设备实例的类名[ **SetupDiGetDeviceRegistryProperty** ](https://msdn.microsoft.com/library/windows/hardware/ff551967)并设置*属性*SPDRP_CLASS 参数。

-   [ **INF InterfaceInstall32 部分**](inf-interfaceinstall32-section.md)包括*InterfaceClassGuid*条目值，用于提供设备接口的 GUID。 此值对应于统一的设备属性模型中的 DEVPKEY_DeviceInterface_ClassGuid 属性。 类可以检索通过查询接口项，也可以通过调用来打开根的子项的已安装的设备接口的 Guid [ **SetupDiOpenClassRegKeyEx** ](https://msdn.microsoft.com/library/windows/hardware/ff552067)并设置*ClassGuid*参数**NULL**并且*标志*DIOCR_INTERFACE 参数。 可以通过调用来检索设备接口的 GUID [ **SetupDiEnumDeviceInterfaces**](https://msdn.microsoft.com/library/windows/hardware/ff551015)，哪些检索[ **SP_DEVICE_INTERFACE_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552342)与设备实例相关联的设备接口的结构。 **InterfaceClassGuid** SP_DEVICE_INTERFACE_DATA 结构成员标识接口的类 GUID。

### <a href="" id="inf-addreg-directives-and-inf-delreg-directives-that-modify-system-def"></a>INF AddReg 指令和修改系统定义的设备属性的 INF DelReg 指令

许多系统定义的设备属性有对应的系统定义的注册表项值。 对于具有相应的注册表条目值，使用的设备属性[ **INF AddReg 指令**](inf-addreg-directive.md)添加相应的注册表项值设置相应的设备属性。 同样，使用[ **INF DelReg 指令**](inf-delreg-directive.md)删除相应的注册表条目值，也会删除相应的设备属性。

例如，INF **AddReg** "Abc_Device_Install.HW"部分，将设置以下指令**DeviceCharacteristics**设备实例的注册表条目值：

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

**DeviceCharacteristics**注册表项值对应于[ **DEVPKEY_Device_Characteristics** ](https://msdn.microsoft.com/library/windows/hardware/ff542375)中的属性[统一的设备属性模型](unified-device-property-model--windows-vista-and-later-.md)Windows Vista 和更高版本的 Windows 中。

### <a href="" id="inf-addreg-directives-and-inf-delreg-directives-that-modify-custom-reg"></a>INF AddReg 指令和修改自定义注册表项值的 INF DelReg 指令

Windows 管理系统定义的注册表条目的值和系统定义的设备属性的对应关系。 但是，Windows 不会管理自定义注册表项值和自定义设备属性之间的对应关系。 [ **INF AddReg 指令**](inf-addreg-directive.md)或[ **INF DelReg 指令**](inf-delreg-directive.md)修改自定义的注册表条目值，不会影响Windows 管理的系统定义的属性。

在下面的示例所示设置的自定义设备实例属性可以通过调用来检索[ **SetupDiGetCustomDeviceProperty**](https://msdn.microsoft.com/library/windows/hardware/ff551099)。

```ini
[XxxDDInstall.HW]
...
AddReg = Xxx_AddReg
...
[Xxx_AddReg]
...
[HKR,,CustomPropertyName,0x10001,0x00000001
] 
```

有关如何访问有对应的自定义注册表项值的自定义设备属性的详细信息，请参阅[访问自定义设备属性](accessing-custom-device-properties.md)。









