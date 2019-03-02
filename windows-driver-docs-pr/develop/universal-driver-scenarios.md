---
title: 通用驱动程序方案
description: 介绍了 DCHU 通用驱动程序示例如何应用 DCHU 设计原则（声明性、组件化、硬件支持应用 [HSA]，以及通用 API 合规性）。
ms.date: 04/04/2018
ms.localizationpriority: medium
ms.openlocfilehash: fdce40f161cdb3eb5a71e6cc01fddb97b0cda50f
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56518190"
---
# <a name="universal-driver-scenarios"></a>通用驱动程序方案

本主题介绍了 [DCHU 通用驱动程序示例](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU)如何应用 DCHU [设计原则](getting-started-with-universal-drivers.md)（声明性、组件化、硬件支持应用 [HSA]，以及通用 API 合规性）。  可以将它用作你自己的通用驱动程序包的模型。

如果你需要此示例存储库的本地副本，请从 [Windows-driver-samples](https://github.com/Microsoft/Windows-driver-samples) 进行克隆。

此示例适用于 Windows 10 版本 1703 和更高版本。

## <a name="prerequisites"></a>先决条件

阅读本部分内容之前，请先查看[通用 Windows 驱动程序入门](getting-started-with-universal-drivers.md)中介绍的通用驱动程序包的要求和最佳做法。

## <a name="overview"></a>概述

DCHU 示例提供了示例情境，其中 Contoso（系统组装商或 OEM）和 Fabrikam（设备制造商或 IHV）这两个硬件合作伙伴合作为 Contoso 即将推出的系统中的设备创建通用 Windows 驱动程序。  有关设备是 [OSR USB FX2 学习工具包](https://store.osr.com/product/osr-usb-fx2-learning-kit-v2/)。  在过去，Fabrikam 会编写针对特定 Contoso 产品线定制的非通用驱动程序包，然后将其交给 OEM 处理服务事宜。  这带来了巨大的维护开销，因此，Fabrikam 决定重构代码，改为创建一个通用驱动程序包。

## <a name="use-only-declarative-sections-and-directives"></a>只使用声明部分和指令

首先，Fabrikam 查看通用驱动程序包中无效的 [INF 部分和指令的列表](../install/using-a-universal-inf-file.md#which-inf-sections-are-invalid-in-a-universal-inf-file)。  在本练习中，Fabrikam 注意到他们在其驱动程序包中使用了这些部分和指令中的很多内容。  

他们的非通用驱动程序 INF 注册了应用平台相关设置和文件的辅助安装程序。  这意味着驱动程序包大于原本应有的容量，并且在 Bug 只影响提供驱动程序的 OEM 系统的某一部分时，更难为驱动程序服务。  另外，大部分 OEM 特定修改与品牌相关，所以每当增加 OEM 或轻微问题影响 OEM 系统的某一部分时，Fabrikam 都需要更新驱动程序包。

Fabrikam 移除了非通用部分和指令，并使用 [InfVerif](../devtest/infverif.md) 工具来验证新驱动程序包的 INF 文件是否是通用的。

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
[OsrUsbFx2_AddReg]
HKR, OSR, "OperatingMode",, "Default" ; FLG_ADDREG_TYPE_SZ
HKR, OSR, "OperatingParams",, "None" ; FLG_ADDREG_TYPE_SZ
```

在 [`osrfx2_DCHU_extension.inx`] 中，Contoso 替代了由基准设定的 **OperatingParams** 注册表值，并添加了 **OperatingExceptions**：

```cpp
[OsrUsbFx2Extension_AddReg]
HKR, OSR, "OperatingParams",, "-Extended"
HKR, OSR, "OperatingExceptions",, "x86" 
```

请注意，在没有明确顺序时，扩展将始终在基准 INF 后进行处理。 如果基准 INF 更新到较新版本，那么扩展仍将在安装新的基准 INF 后重新应用。

## <a name="install-a-service-from-an-inf-file"></a>通过 INF 文件安装服务

Fabrikam 使用 Win32 服务控制 OSR 板上的 LED。 他们将该组件视为设备核心功能的一部分，因此他们在基准 INF ([`osrfx2_DCHU_base.inx`]) 中包含了该组件。  这项用户模式服务 (usersvc) 可通过在 INF 文件中指定 [**AddService**](../install/inf-addservice-directive.md) 指令来以声明方式添加和启动：

```cpp
[OsrFx2_Install.NT]
CopyFiles = OsrFx2_UserSvcCopyFiles

[OsrFx2_Install.NT.Services]
AddService = osrfx2_DCHU_usersvc, 0x00000800, UserSvc_ServiceInstall
    
[UserSvc_ServiceInstall]
DisplayName = %UserSvcDisplayName%
ServiceType = 0x00000010
StartType = 3
ErrorControl = 1
ServiceBinary = %13%\osrfx2_DCHU_usersvc.exe

[OsrFx2_UserSvcCopyFiles]
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

[Win32 应用的源代码](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU/osrfx2_DCHU_extension_loose/osrfx2_DCHU_componentsoftware) 包含在 DCHU 示例中。

请注意，由于 [Windows 硬件开发人员中心仪表板](https://developer.microsoft.com/dashboard/Registration/Hardware)的目标设置，该组件驱动程序包仅可在桌面 SKU 上分发。  有关详细信息，请参阅[将驱动程序发布到 Windows 更新](https://docs.microsoft.com/windows-hardware/drivers/dashboard/publish-a-driver-to-windows-update)。

## <a name="allow-communication-with-a-hardware-support-app"></a>允许与硬件支持应用进行通信

Fabrikam 希望在通用驱动程序包中提供基于 GUI 的伴侣应用。  由于基于 Win32 的伴侣应用程序无法成为通用驱动程序包的一部分，他们将其 Win32 应用转到通用 Windows 平台 (UWP)，并将[应用与设备配对](https://docs.microsoft.com/windows-hardware/drivers/devapps/hardware-access-for-universal-windows-platform-apps)。

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

新应用（不包含在 DCHU 示例中）是安全的，并且可以在 Microsoft Store 内轻松更新。   准备好 UWP 应用程序后，Contoso 使用 [DISM - 部署映像服务和管理](https://docs.microsoft.com/windows-hardware/manufacture/desktop/dism---deployment-image-servicing-and-management-technical-reference-for-windows)在 Windows 桌面版映像上预加载应用程序。

## <a name="registering-a-com-component-in-an-inf-file"></a>在 INF 文件中注册 COM 组件

Fabrikam 需要在不使用辅助安装程序的情况下注册 COM 组件。  为了在通用 INF 文件中实现此目的，他们使用了 WDK 中分发的 [Reg2inf 工具](https://docs.microsoft.com/windows-hardware/drivers/devtest/reg2inf)。  生成 COM 服务器项目（取自[进程内 ATL COM 服务器示例](https://code.msdn.microsoft.com/ATLDllCOMServer-b52a7d5d)）后，他们提供 COM.dll 作为 Reg2inf 工具的输入。  然后，此工具生成 Fabrikam 在其基准 INF ([`osrfx2_DCHU_base.inx`]) 中包含的以下 INF 指令：

```cpp
; Add all registry keys to successfully register the
; In-Process ATL COM Server MSFT Sample.
[OsrFx2_AddReg_COM]
HKCR,AppID\ATLDllCOMServer.DLL,AppID,,"{9DD18FED-55F6-4741-AF25-798B90C4AED5}"
HKCR,AppID\{9DD18FED-55F6-4741-AF25-798B90C4AED5},,,"ATLDllCOMServer"
HKCR,ATLDllCOMServer.SimpleObject,,,"SimpleObject Class"
HKCR,ATLDllCOMServer.SimpleObject\CLSID,,,"{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}"
HKCR,ATLDllCOMServer.SimpleObject\CurVer,,,"ATLDllCOMServer.SimpleObject.1"
HKCR,ATLDllCOMServer.SimpleObject.1,,,"SimpleObject Class"
HKCR,ATLDllCOMServer.SimpleObject.1\CLSID,,,"{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}"
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084},,,"SimpleObject Class"
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}\InprocServer32,,%REG_EXPAND_SZ%,"%%SystemRoot%%\System32\ATLDllCOMServer.dll"
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}\InprocServer32,ThreadingModel,,"Apartment"
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}\ProgID,,,"ATLDllCOMServer.SimpleObject.1"
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}\Programmable,,%FLG_ADDREG_KEYONLY%
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}\TypeLib,,,"{9B23EFED-A0C1-46B6-A903-218206447F3E}"
HKCR,CLSID\{92FCF37F-F6C7-4F8A-AA09-1A14BA118084}\VersionIndependentProgID,,,"ATLDllCOMServer.SimpleObject"
```

## <a name="tightly-coupling-multiple-inf-files"></a>紧密耦合多个 INF 文件

理想的情况下，在基准、扩展和组件之间应存在强有力的版本控制协定。  分别提供这三个程序包（“松散耦合”方案）有其服务优势，但是有时由于版本控制协定不佳，我们需要将这三者捆绑在一个驱动程序包中，这便是“紧密耦合”方案。  示例包含这两种方案的示例：

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

为了使更新驱动程序更加轻松，Fabrikam 尽可能使用 [DirId 13](https://docs.microsoft.com/windows-hardware/drivers/install/using-dirids) 指定[驱动程序存储](../install/driver-store.md)作为要将驱动程序文件复制到的目标。  下面是来自 [`osrfx2_DCHU_base.inx`] 的一个示例：

```cpp
[DestinationDirs]
OsrFx2_UserSvcCopyFiles = 13 ; copy to Driver Store
```

使用目标目录值 13 可以让驱动程序更新过程的稳定性提高。

## <a name="summary"></a>总结

下图显示了 Fabrikam 和 Contoso 为其通用 Windows 驱动程序创建的驱动程序包。  在松散耦合的示例中，他们将在 [Windows 硬件开发人员中心仪表板](https://developer.microsoft.com/dashboard/Registration/Hardware)上分别提交三个包：一个是基准驱动程序包，一个是扩展驱动程序包，还有一个是组件驱动程序包。  在紧密耦合的示例中，他们将提交两个包：基准驱动程序包和扩展/组件驱动程序包。

![扩展、基准和组件驱动程序包](images/universal-scenarios.png)

请注意，组件 INF 将同组件硬件 ID 进行匹配，而基准 INF 和扩展 INF 将同主板硬件 ID 进行匹配。

## <a name="see-also"></a>另请参阅

[通用 Windows 驱动程序入门](getting-started-with-universal-drivers.md)

[使用扩展 INF 文件](../install/using-an-extension-inf-file.md)

[`osrfx2_DCHU_base.inx`]: https://github.com/Microsoft/Windows-driver-samples/blob/master/general/DCHU/osrfx2_DCHU_base/osrfx2_DCHU_base/osrfx2_DCHU_base.inx
[`osrfx2_DCHU_usersvc.inx`]: https://github.com/Microsoft/Windows-driver-samples/blob/master/general/DCHU/osrfx2_DCHU_base/osrfx2_DCHU_usersvc/osrfx2_DCHU_usersvc.inx
[`osrfx2_DCHU_component.inx`]: https://github.com/Microsoft/Windows-driver-samples/blob/master/general/DCHU/osrfx2_DCHU_extension_loose/osrfx2_DCHU_component/osrfx2_DCHU_component.inx
[`osrfx2_DCHU_extension.inx`]: https://github.com/Microsoft/Windows-driver-samples/blob/master/general/DCHU/osrfx2_DCHU_extension_loose/osrfx2_DCHU_extension/osrfx2_DCHU_extension.inx
