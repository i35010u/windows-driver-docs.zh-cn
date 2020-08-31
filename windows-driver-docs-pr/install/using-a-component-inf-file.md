---
title: 使用组件 INF 文件
description: 描述如何使用软件组件包括特定于设备的用户模式软件。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 430f4bf8d4bd7374e48d6167995fed01d9830a1f
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096545"
---
# <a name="using-a-component-inf-file"></a>使用组件 INF 文件

如果要在 Windows 10 上包含用于设备的用户模式软件，可以使用以下选项创建与 [DCH 兼容的驱动程序](../develop/getting-started-with-windows-drivers.md)：
    
|方法|场景|
|---|---|
|[硬件支持应用 (HSA) ](../devapps/hardware-support-app--hsa--steps-for-driver-developers.md) | 作为 UWP 应用打包的设备附加软件，由 Microsoft Store 提供和提供服务。  推荐的方法。 |
|软件组件|设备附加软件是使用 AddReg 和 CopyFiles 安装的 MSI 或 EXE 二进制文件、Win32 服务或软件。  引用的二进制文件仅在桌面版本 (Home、Pro 和 Enterprise) 上运行。  引用的二进制文件将不会在 Windows 数十上运行。|

软件组件是单独的独立驱动程序包，可以安装一个或多个软件模块。  已安装的软件增强了设备的价值，但对于基本设备功能并不需要使用关联的功能驱动程序服务。  

本页提供有关使用软件组件的指南。

## <a name="getting-started"></a>入门

若要创建组件，[扩展 inf 文件](using-an-extension-inf-file.md)会在[inf DDInstall](inf-ddinstall-components-section.md)部分指定[inf AddComponent 指令](inf-addcomponent-directive.md)一次或多次。  对于扩展 INF 文件中引用的每个软件组件，系统将创建一个虚拟软件枚举的子设备。  多个驱动程序包可以引用同一个软件组件。 

只要启动了父设备，虚拟设备子项就可以像任何其他设备一样独立地进行更新。  建议将功能分为多个不同的分组，从维护的角度来看，然后为每个分组创建一个软件组件。

你将为每个软件组件提供一个 INF 文件。

如果软件组件 INF 指定了[ **AddSoftware**指令](inf-addsoftware-directive.md)，则组件 inf：

* 必须是 [通用 INF 文件](../install/using-a-universal-inf-file.md)。
* 必须指定 **SoftwareComponent** 安装程序类。

可以一次或多次指定[ **AddSoftware**指令](inf-addsoftware-directive.md)。

>[!NOTE]
>使用 AddSoftware 指令类型2时，无需使用组件 INF。  指令可以在任何 INF 中成功使用。  但是，必须在组件 INF 中使用类型为1的 AddSoftware 指令。

此外，在软件组件设备上，任何 INF 都 (组件或不) 匹配：

* 可以使用 [AddService 指令](inf-addservice-directive.md)指定 Win32 用户服务。
* 可以使用 [Inf AddReg 指令](inf-addreg-directive.md) 和 [inf CopyFiles 指令](inf-copyfiles-directive.md)安装软件。
* 不需要函数驱动程序服务。
* 用户可以独立于父设备卸载。

可以在 [适用于通用驱动程序的驱动程序包安装工具包](https://github.com/Microsoft/Windows-driver-samples/tree/master/general/DCHU)中找到组件 INF 的示例。

**注意**：为了使软件枚举的组件设备正常运行，必须启动其父项。 如果父设备没有可用的驱动程序，则驱动程序开发人员可以创建自己的驱动程序，并选择性地利用直通驱动程序 "umpass.sys"。 此驱动程序包含在 Windows 中，并且实际上不会启动设备。 为了使用 umpass.sys，开发人员应在每个可能的 [DDInstall] 部分的 [DDInstall 节](inf-ddinstall-section.md) 中使用 Include/UmPass INF 指令 \* \* ，并按如下所示，不管 INF 是否为该部分指定了任何指令：

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

## <a name="accessing-a-device-from-a-software-component"></a>从软件组件访问设备

若要检索与某个软件组件相关联的设备的设备实例 ID，请在[INF AddSoftware 指令](inf-addsoftware-directive.md)部分中使用**SoftwareArguments**值和 `<<DeviceInstanceID>>` 运行时上下文变量。

然后，可执行文件可以从其传入参数列表中检索软件组件的设备实例 ID。  

接下来，如果软件组件以通用 [目标平台](../develop/target-platforms.md)为目标，请使用以下过程：

1. 使用软件组件的设备实例 ID 调用 [**CM_Locate_DevNode**](/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_locate_devnodea) 以检索设备句柄。
2. 调用 [**CM_Get_Parent**](/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_parent) 检索该设备父对象的句柄。  此父级是使用 [INF AddComponent 指令](inf-addcomponent-directive.md)添加软件组件的设备。
3. 然后，若要检索父级的设备实例 ID，请从[**CM_Get_Parent**](/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_parent)中的句柄调用[**CM_Get_Device_ID**](/windows/desktop/api/cfgmgr32/nf-cfgmgr32-cm_get_device_idw) 。

如果软件组件仅以桌面 [目标平台](../develop/target-platforms.md) 为目标，请使用以下过程：

1. 调用 [**SetupDiCreateDeviceInfoList**](/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedeviceinfolist) 创建一个空的设备信息集。
2. 调用具有软件组件设备的设备实例 ID 的 [**SetupDiOpenDeviceInfo**](/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinfoa) 。
3. 调用 [**SetupDiGetDeviceProperty**](/windows/desktop/api/setupapi/nf-setupapi-setupdigetdevicepropertyw) ， `DEVPKEY_Device_Parent` 以检索父的设备实例 ID。

## <a name="example"></a>示例

下面的示例演示如何使用软件组件来安装使用图形卡的可执行文件的 "控制面板"。

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

对于常规 Inf，与组件 Inf 相同的驱动程序验证和提交过程是相同的。 有关详细信息，请参阅 [WINDOWS HLK 入门](/windows-hardware/test/hlk/getstarted/windows-hlk-getting-started)。

有关安装程序类的详细信息，请参阅 [供应商可用的系统定义的设备安装程序类](./system-defined-device-setup-classes-available-to-vendors.md)。

## <a name="see-also"></a>另请参阅

[INF AddComponent 指令](inf-addcomponent-directive.md)

[INF AddSoftware 指令](inf-addsoftware-directive.md)

[INF DDInstall.Components 节](inf-ddinstall-components-section.md)

[INF DDInstall.Software 节](inf-ddinstall-software-section.md)