---
title: DCH 示例
description: 介绍了 DCHU 驱动程序示例如何应用 DCH 设计原则（声明性、组件化、硬件支持应用 [HSA]）。
ms.assetid: f46f0ea6-d855-49d2-8c09-a6ad56084742
ms.date: 04/15/2020
ms.localizationpriority: medium
ms.openlocfilehash: d0894525905e2ecbf5fc3e635a17350fbb91b48e
ms.sourcegitcommit: 4d1ed685d198629f792d287619621a87ca42c26f
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/16/2020
ms.locfileid: "83435379"
---
# <a name="dch-compliant-driver-package-example"></a>符合 DCH 的驱动程序包示例

本主题介绍了 [DCHU 驱动程序示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU)如何应用 [DCH 设计原则](dch-principles-best-practices.md)。  可以将它用作向你自己的驱动程序包应用 DCH 设计原则的模型。  

如果你需要此示例存储库的本地副本，请从 [Windows-driver-samples](https://github.com/Microsoft/Windows-driver-samples) 进行克隆。

此示例的某些部分可能使用只在特定版本的 Windows 10 及更高版本上可用的指令和 API。  若要了解支持给定指令的 OS 版本，请参阅 [INF 指令](../install/inf-directives.md)。

## <a name="prerequisites"></a>必备条件

在阅读本部分之前，应先熟悉 [DCH 设计原则](dch-principles-best-practices.md)。

## <a name="overview"></a>概述

此示例的示例场景为，Contoso（系统组装商或 OEM）和 Fabrikam（设备制造商或 IHV）这两个硬件合作伙伴合作，共同为 Contoso 即将推出的系统中的设备创建符合 DCH 的驱动程序。  有关设备是 [OSR USB FX2 学习工具包](https://go.microsoft.com/fwlink/p/?linkid=2113717)。  在过去，Fabrikam 会编写为特定 Contoso 产品系列自定义的旧驱动程序包，然后将它交给 OEM 来处理服务事宜。  这样做的维护开销巨大，因此 Fabrikam 决定了重构代码，并改为创建符合 DCH 的驱动程序包。

## <a name="use-declarative-sectionsdirectives-and-properly-isolate-inf"></a>使用声明性部分/指令并正确隔离 INF

首先，Fabrikam 审阅符合 DCH 的驱动程序包中无效的 [INF 部分和指令的列表](../install/using-a-universal-inf-file.md#which-inf-sections-are-invalid-in-a-universal-inf-file)。  在本练习中，Fabrikam 注意到他们在其驱动程序包中使用了这些部分和指令中的很多内容。  

他们的驱动程序 INF 注册了辅助安装程序，以应用依赖平台的设置和文件。  这意味着驱动程序包大于原本应有的容量，并且在 Bug 只影响提供驱动程序的 OEM 系统的某一部分时，更难为驱动程序服务。  另外，大部分 OEM 特定修改与品牌相关，所以每当增加 OEM 或轻微问题影响 OEM 系统的某一部分时，Fabrikam 都需要更新驱动程序包。

Fabrikam 删除了非声明性的部分和指令，并使用 [InfVerif](../devtest/infverif.md) 工具来验证新驱动程序包的 INF 文件是否遵循声明性 INF 要求。

## <a name="use-extension-infs-to-componentize-a-driver-package"></a>使用扩展 INF 实现驱动程序包组件化

然后，Fabrikam 将特定于 OEM 合作伙伴（如 Contoso）的自定义项从基准驱动程序包中分离出来，放入[扩展 INF](../install/using-an-extension-inf-file.md)。

以下代码段（从 [`osrfx2_DCHU_extension.inx`] 更新的）指定了 `Extension` 类，并将 Contoso 标识为提供程序，因为它们将拥有扩展驱动程序包：

```cpp
[Version]
Class       = Extension
ClassGuid   = {e2f84ce7-8efa-411c-aa69-97454ca4cb57}
Provider    = Contoso
ExtensionId = {zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz} ; replace with your own GUID
```

在 [`osrfx2_DCHU_base.inx`] 中，Fabrikam 指定了以下条目：

```cpp
[OsrFx2_AddReg]
HKR, OSR, "OperatingMode",, "Default" ; FLG_ADDREG_TYPE_SZ
HKR, OSR, "OperatingParams",, "None" ; FLG_ADDREG_TYPE_SZ
```

在 [`osrfx2_DCHU_extension.inx`] 中，Contoso 替代了由基准设定的 **OperatingParams** 注册表值，并添加了 **OperatingExceptions**：

```cpp
[OsrFx2Extension_AddReg]
HKR, OSR, "OperatingParams",, "-Extended"
HKR, OSR, "OperatingExceptions",, "x86"
```

请注意，扩展总是在基础 INF 之后处理，但没有确定的顺序。 如果基准 INF 更新到较新版本，那么扩展仍将在安装新的基准 INF 后重新应用。

## <a name="install-a-service-from-an-inf-file"></a>通过 INF 文件安装服务

Fabrikam 使用 Win32 服务控制 OSR 板上的 LED。 他们将该组件视为设备核心功能的一部分，因此他们在基准 INF ([`osrfx2_DCHU_base.inx`]) 中包含了该组件。  这项用户模式服务 (usersvc) 可通过在 INF 文件中指定 [**AddService**](../install/inf-addservice-directive.md) 指令来以声明方式添加和启动：

```cpp
[OsrFx2_Install.NT]
CopyFiles = OsrFx2_CopyFiles

[OsrFx2_Install.NT.Services]
AddService = WUDFRd, 0x000001fa, WUDFRD_ServiceInstall    ; Flag 0x2 sets this as the service for the device
AddService = osrfx2_DCHU_usersvc,, UserSvc_ServiceInstall

[UserSvc_ServiceInstall]
DisplayName = %UserSvcDisplayName%
ServiceType = 0x10                                ; SERVICE_WIN32_OWN_PROCESS
StartType = 0x3                                   ; SERVICE_DEMAND_START
ErrorControl = 0x1                                ; SERVICE_ERROR_NORMAL
ServiceBinary = %13%\osrfx2_DCHU_usersvc.exe
AddTrigger = UserSvc_AddTrigger                   ; AddTrigger syntax is only available in Windows 10 Version 2004 and above

[UserSvc_AddTrigger]
TriggerType = 1                                   ; SERVICE_TRIGGER_TYPE_DEVICE_INTERFACE_ARRIVAL
Action = 1                                        ; SERVICE_TRIGGER_ACTION_SERVICE_START
SubType = %GUID_DEVINTERFACE_OSRFX2%              ; Interface GUID
DataItem = 2, "USB\VID_0547&PID_1002"             ; SERVICE_TRIGGER_DATA_TYPE_STRING

[OsrFx2_CopyFiles]
osrfx2_DCHU_base.dll
osrfx2_DCHU_filter.dll
osrfx2_DCHU_usersvc.exe
```

请注意，这项服务还可以安装在组件或扩展 INF 中，具体取决于所用方案。

## <a name="use-a-component-to-install-legacy-software-from-a-driver-package"></a>使用组件从驱动程序包安装旧软件

Fabrikam 有一个之前使用辅助安装程序安装的可执行文件 `osrfx2_DCHU_componentsoftware.exe`。  此旧软件显示由开发板设置且 OEM 需要的注册表项。  这是一个基于 GUI 的可执行文件，它只在 Windows 桌面版上运行。  为了安装此文件，Fabrikam 创建了一个单独的组件驱动程序包，并将其添加在扩展 INF 中。

来自 [`osrfx2_DCHU_extension.inx`] 的以下片段使用 [**AddComponent**](../install/inf-addcomponent-directive.md) 指令来创建虚拟子设备：

```cpp
[OsrFx2Extension_Install.NT.Components]
AddComponent = osrfx2_DCHU_component,,OsrFx2Extension_ComponentInstall


[OsrFx2Extension_ComponentInstall]
ComponentIds=VID_045e&PID_94ab
```

然后，在组件 INF [`osrfx2_DCHU_component.inx`] 中，Fabrikam 指定 [**AddSoftware**](../install/inf-addsoftware-directive.md) 指令来安装可选的可执行文件：

```cpp
[OsrFx2Component_Install.NT.Software]
AddSoftware = osrfx2_DCHU_componentsoftware,, OsrFx2Component_SoftwareInstall

[OsrFx2Component_SoftwareInstall]
SoftwareType = 1
SoftwareBinary = osrfx2_DCHU_componentsoftware.exe
SoftwareArguments = <<DeviceInstanceId>>
SoftwareVersion = 1.0.0.0

[OsrFx2Component_CopyFiles]
osrfx2_DCHU_componentsoftware.exe
```

此示例包含了 [Win32 应用的源代码](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU/osrfx2_DCHU_extension_loose/osrfx2_DCHU_componentsoftware)。

请注意，由于 [Windows 硬件开发人员中心仪表板](https://partner.microsoft.com/dashboard/Registration/Hardware)的目标设置，该组件驱动程序包仅可在桌面 SKU 上分发。  有关详细信息，请参阅[将驱动程序发布到 Windows 更新](https://docs.microsoft.com/windows-hardware/drivers/dashboard/publish-a-driver-to-windows-update)。

## <a name="allow-communication-with-a-hardware-support-app"></a>允许与硬件支持应用进行通信

Fabrikam 要提供基于 GUI 的伴侣应用，作为 Windows 驱动程序包的一部分。  由于基于 Win32 的伴侣应用无法成为 Windows 驱动程序包的一部分，因此他们将 Win32 应用移植到通用 Windows 平台 (UWP)，并将[应用与设备配对](https://docs.microsoft.com/windows-hardware/drivers/devapps/hardware-access-for-universal-windows-platform-apps)。

来自 [`osrfx2_DCHU_base/device.c`](https://github.com/Microsoft/Windows-driver-samples/blob/master/general/DCHU/osrfx2_DCHU_base/osrfx2_DCHU_base/device.c) 的以下片段显示基准驱动程序包如何将自定义功能添加到设备接口实例：

```cpp
    WDF_DEVICE_INTERFACE_PROPERTY_DATA PropertyData = { 0 };
    static const wchar_t customCapabilities[] = L"CompanyName.yourCustomCapabilityNameTBD_YourStorePubId\0";

    WDF_DEVICE_INTERFACE_PROPERTY_DATA_INIT(&PropertyData,
                                            &GUID_DEVINTERFACE_OSRUSBFX2,
                                            &DEVPKEY_DeviceInterface_UnrestrictedAppCapabilities);

    Status = WdfDeviceAssignInterfaceProperty(Device,
                                              &PropertyData,
                                              DEVPROP_TYPE_STRING_LIST,
                                              sizeof(customCapabilities),
                                              (PVOID)customCapabilities);
```

这个新应用（不包含在此示例中）是安全的，并且可以在 Microsoft Store 中轻松更新。 在 UWP 应用就绪后，Contoso 使用 [DISM - 部署映像服务和管理](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism---deployment-image-servicing-and-management-technical-reference-for-windows)在 Windows 桌面版映像上预加载应用。

## <a name="tightly-coupling-multiple-inf-files"></a>紧密耦合多个 INF 文件

理想情况下，在基础、扩展和组件之间应有强大的版本控制协定。  分别提供这三个程序包（“松散耦合”方案）有其服务优势，但是有时由于版本控制协定不佳，我们需要将这三者捆绑在一个驱动程序包中，这便是“紧密耦合”方案。  示例包含这两种方案的示例：

* [DCHU_Sample\osrfx2_DCHU_extension_loose](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU/osrfx2_DCHU_extension_loose)
* [DCHU_Sample\osrfx2_DCHU_extension_tight](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU/osrfx2_DCHU_extension_tight)

  如果扩展和组件位于同一个驱动程序包中（“紧密耦合”），则扩展 INF 指定 [CopyINF 指令](../install/inf-copyinf-directive.md)以便将组件 INF 复制到目标系统。  这在 [DCHU_Sample\osrfx2_DCHU_extension_tight\osrfx2_DCHU_extension\osrfx2_DCHU_extension.inx](https://github.com/Microsoft/Windows-driver-samples/blob/master/general/DCHU/osrfx2_DCHU_extension_tight/osrfx2_DCHU_extension/osrfx2_DCHU_extension.inx) 中进行了演示：

```cpp
[OsrFx2Extension_Install.NT]
CopyInf=osrfx2_DCHU_component.inf
```

该指令还可用于协调在多功能设备上安装 INF 文件。  有关更多详细信息，请参阅[复制 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/copying-inf-files)。

> [!NOTE]
> 虽然基本驱动程序可以装载一个扩展（并以发货标签中的基本驱动程序为目标），但是无法将与另一个驱动程序捆绑的扩展发布到扩展硬件 ID。

## <a name="run-from-the-driver-store"></a>从驱动程序存储运行

为了更容易地更新驱动程序，Fabrikam 尽可能使用 [dirid 13](../install/using-dirids.md)，以指定[驱动程序存储](../install/driver-store.md)作为复制驱动程序文件的目标。  使用目标目录值 13 可以让驱动程序更新过程的稳定性提高。  下面是来自 [`osrfx2_DCHU_base.inx`] 的一个示例：

```cpp
[DestinationDirs]
OsrFx2_CopyFiles = 13 ; copy to Driver Store
```

若要详细了解如何从驱动程序存储中动态查找和加载文件，请参阅[驱动程序包隔离](driver-isolation.md#run-from-driver-store)页。  

## <a name="summary"></a>摘要

下图展示了 Fabrikam 和 Contoso 为符合 DCH 的驱动程序创建的驱动程序包。  在松散耦合的示例中，他们将在 [Windows 硬件开发人员中心仪表板](https://partner.microsoft.com/dashboard/Registration/Hardware)上分别提交三个包：一个是基准驱动程序包，一个是扩展驱动程序包，还有一个是组件驱动程序包。  在紧密耦合的示例中，他们将提交两个包：基准驱动程序包和扩展/组件驱动程序包。

![扩展、基准和组件驱动程序包](images/universal-scenarios.png)

请注意，组件 INF 将同组件硬件 ID 进行匹配，而基准 INF 和扩展 INF 将同主板硬件 ID 进行匹配。

## <a name="see-also"></a>另请参阅

[Windows 驱动程序入门](getting-started-with-windows-drivers.md)

[使用扩展 INF 文件](../install/using-an-extension-inf-file.md)

[`osrfx2_DCHU_base.inx`]: https://github.com/Microsoft/Windows-driver-samples/blob/master/general/DCHU/osrfx2_DCHU_base/osrfx2_DCHU_base/osrfx2_DCHU_base.inx

[`osrfx2_DCHU_usersvc.inx`]: https://github.com/Microsoft/Windows-driver-samples/blob/master/general/DCHU/osrfx2_DCHU_base/osrfx2_DCHU_usersvc/osrfx2_DCHU_usersvc.inx

[`osrfx2_DCHU_component.inx`]: https://github.com/Microsoft/Windows-driver-samples/blob/master/general/DCHU/osrfx2_DCHU_extension_loose/osrfx2_DCHU_component/osrfx2_DCHU_component.inx

[`osrfx2_DCHU_extension.inx`]: https://github.com/Microsoft/Windows-driver-samples/blob/master/general/DCHU/osrfx2_DCHU_extension_loose/osrfx2_DCHU_extension/osrfx2_DCHU_extension.inx
