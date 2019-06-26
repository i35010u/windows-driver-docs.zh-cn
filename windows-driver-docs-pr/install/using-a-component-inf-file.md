---
title: 使用组件 INF 文件
description: 介绍如何使用软件组件包括特定于设备的用户模式软件。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: eeda366397fc82430a1667da4adaebdddf872cbb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67380449"
---
# <a name="using-a-component-inf-file"></a>使用组件 INF 文件

如果你想要使用 Windows 10 上的设备包括使用用户模式软件，具有以下选项来创建[DCHU 符合通用驱动程序](../develop/getting-started-with-universal-drivers.md):
    
|方法|应用场景|
|---|---|
|[硬件支持应用程序 (HSA)](../devapps/hardware-support-app--hsa--steps-for-driver-developers.md) | 打包为 UWP 应用的交付和从 Microsoft Store 中处理的设备外接程序软件。  建议的方法。 |
|软件组件|MSI 或 EXE 的二进制文件、 Win32 服务或使用 AddReg 和 CopyFiles 安装的软件，设备外接程序软件。  引用的二进制文件仅在桌面版本中 （主页、 Pro 和 Enterprise） 上运行。  引用的二进制文件将不运行在 Windows 10 秒。|

软件组件是相互独立的独立驱动程序包可以安装一个或多个软件模块。  已安装的软件增强了设备的值，但不是有基本的设备功能必需的不需要关联的函数驱动程序服务。  

此页使用的软件组件提供了指导原则。

## <a name="getting-started"></a>即刻体验

若要创建的组件，[扩展 INF 文件](using-an-extension-inf-file.md)指定[INF AddComponent 指令](inf-addcomponent-directive.md)中的一个或多个时间[INF DDInstall.Components](inf-ddinstall-components-section.md)部分。  对于每个扩展 INF 文件中引用的软件组件，系统会创建虚拟软件枚举子设备。  多个驱动程序包可以引用相同的软件组件。 

虚拟设备子级可独立更新就像任何其他设备一样，只要父设备已启动。  我们建议将分离分为任意多个不同的组，如从服务角度来看，并创建一个软件组件，为每个分组有意义的功能。

你将提供每个软件组件的 INF 文件。

如果指定了你的软件组件 INF [ **AddSoftware**指令](inf-addsoftware-directive.md)，组件 INF:

* 必须是[通用 INF 文件](../install/using-a-universal-inf-file.md)。
* 必须指定**SoftwareComponent**安装程序类。

您可以指定[ **AddSoftware**指令](inf-addsoftware-directive.md)的一个或多个时间。

>[!NOTE]
>在使用类型 2 的 AddSoftware 指令，它不需要利用组件 INF。  指令可在任何 INF 成功。  键入 1，一个 AddSoftware 指令但是，必须使用从组件 INF。

此外，任何 INF (组件或不) 匹配的软件组件设备上：

* 可以使用 Win32 用户服务指定[AddService 指令](inf-addservice-directive.md)。
* 可以安装软件，在使用[INF AddReg 指令](inf-addreg-directive.md)并[INF CopyFiles 指令](inf-copyfiles-directive.md)。
* 不需要函数驱动程序服务。
* 可以通过独立于父设备用户卸载。

可以找到举例说明在组件 INF[驱动程序的通用驱动程序的包安装工具包](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU)。

**注意**：为了使软件枚举组件设备函数，必须启动其父级。 如果不没有可用于父设备的任何驱动程序，驱动程序开发人员可以创建他们自己，并选择性地利用直通驱动程序"umpass.sys"。 此驱动程序包含在 Windows 中，并有效地启动不执行任何操作而不启动设备。 若要使用 umpass.sys，开发人员应使用中的 Include/Needs INF 指令[DDInstall 部分](inf-ddinstall-section.md)对于每个可能的 [DDInstall。\*] 到相应的部分 [UmPass。\*] 部分，如所示下面，而不考虑是否 INF 指定该部分的任何指令或不：

```cpp
[DDInstall]
Include=umpass.inf
Needs=UmPass
; also include any existing DDInstall directives

[DDInstall.HW]
Include=umpass.inf
Needs=UmPass.HW
; also include any existing DDInstall.HW directives

[DDInstall.Interfaces]
Include=umpass.inf
Needs=UmPass.Interfaces
; also include any existing DDInstall.Interfaces directives

[DDInstall.Services]
Include=umpass.inf
Needs=UmPass.Services
; also include any existing any DDInstall.Services directives
```

## <a name="accessing-a-device-from-a-software-component"></a>从软件组件访问的设备

若要检索的软件组件与相关联的设备的设备实例 ID，请使用**SoftwareArguments**中的值[INF AddSoftware 指令](inf-addsoftware-directive.md)部分`<<DeviceInstanceID>>`运行时上下文变量。

然后，可执行文件可以从其传入的参数列表来检索软件组件的设备实例 ID。  

接下来，如果软件组件定目标到通用[目标平台](../develop/windows-10-editions-for-universal-drivers.md)，使用以下过程：

1. 调用[ **CM_Locate_DevNode** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_locate_devnodea)与设备实例 ID 的软件组件，以检索设备句柄。
2. 调用[ **CM_Get_Parent** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_parent)检索到该设备的父级的句柄。  此父级是软件组件使用添加的设备[INF AddComponent 指令](inf-addcomponent-directive.md)。
3. 然后，若要检索父级的设备实例 ID，请调用[ **CM_Get_Device_ID** ](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_device_idw)从句柄上[ **CM_Get_Parent**](https://docs.microsoft.com/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_parent)。

如果软件组件面向桌面[目标平台](../develop/windows-10-editions-for-universal-drivers.md)只，请使用以下过程：

1. 调用[ **SetupDiCreateDeviceInfoList** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinfolist)若要创建空的设备信息设置。
2. 调用[ **SetupDiOpenDeviceInfo** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinfoa)与软件组件设备的设备实例 id。
3. 调用[ **SetupDiGetDeviceProperty** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw)与`DEVPKEY_Device_Parent`要检索父级的设备实例 ID。

## <a name="example"></a>示例

下面的示例演示如何使用软件组件安装可执行文件用于图形卡的控制面板。

### <a name="driver-package-inf-file"></a>驱动程序包 INF 文件

```cpp
[Version]
Signature   = "$WINDOWS NT$"
Class       = Extension
ClassGuid   = {e2f84ce7-8efa-411c-aa69-97454ca4cb57}
ExtensionId = {zzzzzzzz-zzzz-zzzz-zzzz-zzzzzzzzzzzz} ; replace with your own GUID
Provider    = %CONTOSO%
DriverVer   = 06/21/2006,1.0.0.0
CatalogFile = ContosoGrfx.cat

[Manufacturer]
%CONTOSO%=Contoso,NTx86

[Contoso.NTx86]
%ContosoGrfx.DeviceDesc%=ContosoGrfx, PCI\VEN0001&DEV0001

[ContosoGrfx.NT]
;empty

[ContosoGrfx.NT.Components]
AddComponent = ContosoControlPanel,, Component_Inst

[Component_Inst]
ComponentIDs = VID0001&PID0001&SID0001

[Strings]
CONTOSO = "Contoso Inc."
ContosoGrfx.DeviceDesc = "Contoso Graphics Card Extension"
```

### <a name="software-component-inf-file"></a>软件组件 INF 文件

```cpp
[Version]
Signature   = "$WINDOWS NT$"
Class       = SoftwareComponent
ClassGuid   = {5c4c3332-344d-483c-8739-259e934c9cc8}
Provider    = %CONTOSO%
DriverVer   = 06/21/2006,1.0.0.0
CatalogFile = ContosoCtrlPnl.cat

[SourceDisksNames]
1 = %Disk%,,,""

[SourceDisksFiles]
ContosoCtrlPnl.exe = 1

[DestinationDirs]
DefaultDestDir = 13

[Manufacturer]
%CONTOSO%=Contoso,NTx86

[Contoso.NTx86]
%ContosoCtrlPnl.DeviceDesc%=ContosoCtrlPnl, SWC\VID0001&PID0001&SID0001

[ContosoCtrlPnl.NT]
CopyFiles=ContosoCtrlPnl.NT.Copy

[ContosoCtrlPnl.NT.Copy]
ContosoCtrlPnl.exe

[ContosoCtrlPNl.NT.Services]
AddService = , %SPSVCINST_ASSOCSERVICE%

[ContosoCtrlPnl.NT.Software]
AddSoftware = ContosoGrfx1CtrlPnl,, Software_Inst

[Software_Inst]
SoftwareType = 1
SoftwareBinary = %13%\ContosoCtrlPnl.exe
SoftwareArguments = <<DeviceInstanceID>>
SoftwareVersion = 1.0.0.0

[Strings]
SPSVCINST_ASSOCSERVICE = 0x00000002
CONTOSO = "Contoso"
ContosoCtrlPnl.DeviceDesc = "Contoso Control Panel" 
```

驱动程序验证和提交过程是相同的组件与正则 Inf Inf。 有关详细信息，请参阅[Windows HLK Getting Started](https://docs.microsoft.com/windows-hardware/test/hlk/getstarted/windows-hlk-getting-started)。

安装程序类的详细信息，请参阅[系统定义设备安装程序类可用于供应商](https://docs.microsoft.com/windows-hardware/drivers/install/system-defined-device-setup-classes-available-to-vendors)。

## <a name="see-also"></a>请参阅

[INF AddComponent 指令](inf-addcomponent-directive.md)

[INF AddSoftware 指令](inf-addsoftware-directive.md)

[INF DDInstall.Components 部分](inf-ddinstall-components-section.md)

[INF DDInstall.Software 部分](inf-ddinstall-software-section.md)
