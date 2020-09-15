---
title: 在 Windows Vista 之前修改设备属性的 INF 文件输入值
description: 在 Windows Vista 之前修改设备属性的 INF 文件输入值
ms.assetid: b2a1f265-fc9b-47fb-83af-b4f66d79da83
keywords:
- 设备属性 WDK 设备安装，修改
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: acbef8c95838847fb9208e4f4a6dfc1825131115
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90103340"
---
# <a name="inf-file-entry-values-that-modify-device-properties-before-windows-vista"></a>在 Windows Vista 之前修改设备属性的 INF 文件输入值


以下是在 Windows Server 2003、Windows XP 和 Windows 2000 上修改设备属性的 INF 文件条目值：

-   INF 文件输入值，用于设置设备属性，这些属性对应于 Windows Vista 和更高版本的 Windows 中的[统一设备属性模型](unified-device-property-model--windows-vista-and-later-.md)所包含的[系统定义的设备属性](/previous-versions/ff553413(v=vs.85))。

-   [**Inf AddReg 指令**](inf-addreg-directive.md) 和 [**inf DelReg 指令**](inf-delreg-directive.md) ，用于设置或删除系统定义的注册表项值，这些值对应于 Windows Vista 和更高版本中统一设备属性模型所包含的系统定义的设备属性。

-   INF **AddReg** 指令和 inf **DelReg** 指令，用于设置或删除与自定义设备属性对应的自定义注册表项值。

有关安装设备实例、 [设备安装程序类](./overview-of-device-setup-classes.md)、 [设备接口类](./overview-of-device-interface-classes.md)和设备接口的 INF 文件部分的常规信息，请参阅以下主题：

[**INF *DDInstall* 部分**](inf-ddinstall-section.md)

[**INF ClassInstall32 节**](inf-classinstall32-section.md)

[**INF InterfaceInstall32 节**](inf-interfaceinstall32-section.md)

[**INF *DDInstall*。接口部分**](inf-ddinstall-interfaces-section.md)

### <a name="inf-file-entry-values-that-correspond-to-system-defined-device-properties"></a><a href="" id="inf-file-entry-values-that-correspond-to-system-defined-device-propert"></a>与系统定义的设备属性相对应的 INF 文件输入值

某些 INF 文件输入值提供 Windows 用于设置与设备实例属性和设备接口属性相对应的系统定义注册表项值的信息。 以下是此类 INF 文件条目值提供的注册表项值的几个示例：

-   INF 文件的 [**Inf 型号部分**](inf-models-section.md) 包含 *设备说明* 条目值。 此值对应于统一设备属性模型中的 [**DEVPKEY_Device_DeviceDesc**](./devpkey-device-devicedesc.md) 属性，可通过调用 [**SetupDiGetDeviceRegistryProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya) 并将 *属性* 参数设置为 SPDRP_DEVICEDESC 来检索。

-   [**Inf 版本部分**](inf-version-section.md)的 inf**类**指令包括*类名称*输入值，该值提供[设备安装程序类](./overview-of-device-setup-classes.md)的名称。 此值对应于统一设备属性模型中的 [**DEVPKEY_DeviceClass_ClassName**](./devpkey-deviceclass-classname.md) 属性。 设备安装程序类的类名称可以通过调用 [**SetupDiClassNameFromGuid**](/windows/desktop/api/setupapi/nf-setupapi-setupdiclassnamefromguida)进行检索，并且可以通过调用 [**SetupDiGetDeviceRegistryProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdeviceregistrypropertya) 检索设备实例的类名，并将 *Property* 参数设置为 SPDRP_CLASS。

-   [**INF InterfaceInstall32 部分**](inf-interfaceinstall32-section.md)包括一个*InterfaceClassGuid*条目值，该值提供设备接口的 GUID。 此值对应于统一设备属性模型中的 DEVPKEY_DeviceInterface_ClassGuid 属性。 可以通过查询接口键的根的子项来检索已安装的设备接口类的 Guid，可以通过调用 [**SetupDiOpenClassRegKeyEx**](/windows/desktop/api/setupapi/nf-setupapi-setupdiopenclassregkeyexa) 打开该接口的根子项，并将 *ClassGuid* 参数设置为 **NULL** ，并将 *Flags* 参数设置为 DIOCR_INTERFACE。 可以通过调用 [**SetupDiEnumDeviceInterfaces**](/windows/desktop/api/setupapi/nf-setupapi-setupdienumdeviceinterfaces)来检索设备接口的 GUID，该接口将检索与设备实例关联的设备接口的 [**SP_DEVICE_INTERFACE_DATA**](/windows/win32/api/setupapi/ns-setupapi-sp_device_interface_data) 结构。 SP_DEVICE_INTERFACE_DATA 结构的 **InterfaceClassGuid** 成员标识接口类 GUID。

### <a name="inf-addreg-directives-and-inf-delreg-directives-that-modify-system-defined-device-properties"></a><a href="" id="inf-addreg-directives-and-inf-delreg-directives-that-modify-system-def"></a>用于修改系统定义的设备属性的 INF AddReg 指令和 INF DelReg 指令

许多系统定义的设备属性具有相应的系统定义的注册表项值。 对于具有相应注册表项值的设备属性，使用 [**INF AddReg 指令**](inf-addreg-directive.md) 添加相应的注册表项值将设置相应的设备属性。 同样，使用 [**INF DelReg 指令**](inf-delreg-directive.md) 删除相应的注册表项值，也会删除相应的设备属性。

例如，以下 "Abc_Device_Install HW" 部分中的 INF **AddReg** 指令将设置设备实例的 **DeviceCharacteristics** 注册表项值：

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

**DeviceCharacteristics**注册表项值对应于 windows Vista 和更高版本的 windows 中的[统一设备属性模型](unified-device-property-model--windows-vista-and-later-.md)中的[**DEVPKEY_Device_Characteristics**](./devpkey-device-characteristics.md)属性。

### <a name="inf-addreg-directives-and-inf-delreg-directives-that-modify-custom-registry-entry-values"></a><a href="" id="inf-addreg-directives-and-inf-delreg-directives-that-modify-custom-reg"></a>用于修改自定义注册表项值的 INF AddReg 指令和 INF DelReg 指令

Windows 管理系统定义的注册表项值和系统定义的设备属性之间的对应关系。 但是，Windows 不会管理自定义注册表项值和自定义设备属性之间的对应关系。 用于修改自定义注册表项值的 [**Inf AddReg 指令**](inf-addreg-directive.md) 或 [**inf DelReg 指令**](inf-delreg-directive.md) 不影响 Windows 所管理的系统定义的属性。

如以下示例中所示，可通过调用 [**SetupDiGetCustomDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetcustomdevicepropertya)来检索自定义设备实例属性，如下面的示例中所示。

```inf
[XxxDDInstall.HW]
...
AddReg = Xxx_AddReg
...
[Xxx_AddReg]
...
[HKR,,CustomPropertyName,0x10001,0x00000001
] 
```

有关如何访问具有相应自定义注册表项值的自定义设备属性的详细信息，请参阅 [访问自定义设备属性](accessing-custom-device-properties.md)。