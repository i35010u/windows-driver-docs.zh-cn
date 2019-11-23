---
Description: 将设备的内核模式堆栈中的 WinUSB （Winusb）安装为 USB 设备的函数驱动程序，而不是实现驱动程序。
title: WinUSB (Winusb.sys) 安装
ms.date: 05/09/2018
ms.localizationpriority: High
ms.openlocfilehash: d2157430a1e220e693d9ae88c3a3a36ce3fd3d2e
ms.sourcegitcommit: c73954a5909ec8c7e189f77fd5813f2eb749687c
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2019
ms.locfileid: "72007589"
---
# <a name="winusb-winusbsys-installation"></a>WinUSB (Winusb.sys) 安装


对于某些通用串行总线（USB）设备，例如仅由单个应用程序访问的设备，你可以将设备的内核模式堆栈中的[WinUSB](winusb.md) （WinUSB）安装为 USB 设备的函数驱动程序，而不是实现驱动程序。

本主题包含以下部分：

-   [不使用 INF 文件自动安装 WinUSB](#automatic-installation-of--winusb-without-an-inf-file)
-   [通过指定系统提供的设备类来安装 WinUSB](#installing-winusb-by-specifying--the-system-provided-device-class)
-   [为 WinUSB 安装编写自定义 INF](#inf)
-   [如何创建驱动程序包以安装 Winusb](#howto)

## <a href="" id="automatic-installation-of--winusb-without-an-inf-file"></a>不使用 INF 文件自动安装 WinUSB


作为 OEM 或独立硬件供应商（IHV），可以构建设备，以便在 Windows 8 和更高版本的操作系统上自动安装 Winusb。 此类设备称为 WinUSB 设备，无需编写引用内置 Winusb 的自定义 INF 文件。

连接 WinUSB 设备时，系统会自动读取设备信息并加载 Winusb。

有关详细信息，请参阅[WinUSB 设备](automatic-installation-of-winusb.md)。

## <a href="" id="installing-winusb-by-specifying--the-system-provided-device-class"></a>通过指定系统提供的设备类来安装 WinUSB


连接设备时，可能会注意到，Windows 会自动加载 Winusb （如果 IHV 已将设备定义为 WinUSB 设备）。 否则，请按照以下说明加载该驱动程序：

1.  将设备插入主机系统。
2.  打开设备管理器并找到设备。
3.  右键单击该设备，然后从上下文菜单中选择 "**更新驱动程序软件 ...** "。
4.  在向导中，选择 "**浏览计算机以查找驱动程序软件**"。
5.  选择 **"让我从计算机上的设备驱动程序列表中**选择"。
6.  从设备类的列表中，选择 "**通用串行总线设备**"。
7.  向导将显示 " **WinUsb 设备**"。 选择它以加载驱动程序。

如果 "**通用串行总线设备**" 未出现在设备类列表中，则需要使用自定义 INF 安装该驱动程序。
前面的过程不会为应用（UWP 应用或 Windows 桌面应用）添加设备接口 GUID 来访问设备。 必须按照此过程手动添加 GUID。

1.  按照前面的过程中所述加载驱动程序。
2.  使用 guidgen.exe 等工具生成设备的设备接口 GUID。
3.  查找此项下的设备的注册表项：

    **HKEY\_本地\_计算机\\系统\\CurrentControlSet\\枚举\\USB\\&lt;VID\_vvvv & PID\_pppp&gt;**

4.  在**Device Parameters**项下，添加名为**DeviceInterfaceGUID**的字符串注册表项或名为**DeviceInterfaceGUIDs**的多字符串项。 将值设置为在步骤2中生成的 GUID。
5.  断开设备与系统的连接，并将其重新连接到同一个物理端口。
    **请注意**  如果更改物理端口，则必须重复步骤1到4。

     

## <a href="" id="inf"></a>为 WinUSB 安装编写自定义 INF


作为驱动程序包的一部分，你提供了一个 .inf 文件，该文件将 Winusb 安装为 USB 设备的函数驱动程序。

以下示例 .inf 文件显示了 WinUSB 安装，其中包含一些修改，例如将**usb\_安装**在节名称中，更改为相应的*DDInstall*值。 如果需要，还应更改版本、制造商和型号部分。 例如，提供适当制造商的名称、签名的目录文件的名称、正确的设备类以及设备的供应商标识符（VID）和产品标识符（PID）。

另请注意，安装程序类设置为 "USBDevice"。 对于不属于其他类且不是 USB 主机控制器或集线器的设备，供应商可以使用 "USBDevice" 安装程序类。

如果要将 WinUSB 安装为 USB 复合设备中某个函数的函数驱动程序，则必须在 INF 中提供与该函数关联的硬件 ID。 可以从**设备管理器**中的 devnode 的属性获取该函数的硬件 ID。 硬件 ID 字符串格式为 "USB\\VID\_vvvv & PID\_pppp"。

以下 INF 在基于 x64 的系统上将 WinUSB 安装为 OSR USB FX2 板的函数驱动程序。

> 从 Windows 10 1709 版开始，Windows 驱动程序工具包提供了可用于测试驱动程序 INF 文件的[InfVerif](https://docs.microsoft.com/windows-hardware/drivers/devtest/infverif) ，以确保不存在任何语法问题并且 INF 文件是通用的。 我们推荐您提供了通用 INF。 有关详细信息，请参阅[使用通用 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/using-a-universal-inf-file)。

``` syntax
;
;
; Installs WinUsb
;

[Version]
Signature = "$Windows NT$"
Class     = USBDevice
ClassGUID = {88BAE032-5A81-49f0-BC3D-A4FF138216D6}
Provider  = %ManufacturerName%
CatalogFile = WinUSBInstallation.cat
DriverVer=09/04/2012,13.54.20.543

; ========== Manufacturer/Models sections ===========

[Manufacturer]
%ManufacturerName% = Standard,NTamd64

[Standard.NTamd64]
%DeviceName% =USB_Install, USB\VID_0547&PID_1002

; ========== Class definition (for Windows 8 and ealier versions)===========

[ClassInstall32]
AddReg = ClassInstall_AddReg

[ClassInstall_AddReg]
HKR,,,,%ClassName%
HKR,,NoInstallClass,,1
HKR,,IconPath,%REG_MULTI_SZ%,"%systemroot%\system32\setupapi.dll,-20"
HKR,,LowerLogoVersion,,5.2

; =================== Installation ===================

[USB_Install]
Include = winusb.inf
Needs   = WINUSB.NT

[USB_Install.Services]
Include =winusb.inf
Needs   = WINUSB.NT.Services

[USB_Install.HW]
AddReg=Dev_AddReg

[USB_Install.Wdf]
KmdfService=WINUSB, WinUsb_Install

[WinUsb_Install]
KmdfLibraryVersion=1.11

[Dev_AddReg]
HKR,,DeviceInterfaceGUIDs,0x10000,"{9f543223-cede-4fa3-b376-a25ce9a30e74}"

; [DestinationDirs]
; If your INF needs to copy files, you must not use the DefaultDestDir directive here.  
; You must explicitly reference all file-list-section names in this section.

; =================== Strings ===================

[Strings]
ManufacturerName=""
ClassName="Universal Serial Bus devices"
DeviceName="Fx2 Learning Kit Device"
REG_MULTI_SZ = 0x00010000
```
> 仅在设备 INF 文件中包含 ClassInstall32 部分，以安装新的自定义设备安装程序类。 已安装类中的设备的 INF 文件，无论系统提供的设备安装程序类还是自定义类，都不得包含 ClassInstall32 部分。 




除了特定于设备的值以及以下列表中所述的几个问题之外，你可以使用这些部分和指令来安装适用于任何 USB 设备的 WinUSB。 这些列表项描述了前面的 .inf 文件中的**包含**和**指令**。

-   **Usb\_安装**：在安装 WinUSB 时，需要在**usb\_安装**部分中**包含**和**需要**指令。 不应修改这些指令。
-   **Usb\_install**： WinUSB **\_** 中的 Include 指令包括 WinUSB （）的系统提供的 .inf 中的**Include**指令。 此 .inf 文件由 WinUSB 联安装程序安装（如果它尚未在目标系统上）。 Required**指令指定 WinUSB 中的部分**，其中包含安装 WinUSB 作为设备的函数驱动程序所需的信息。 不应修改这些指令。
    **请注意**  由于 windows xp 不提供 WinUSB，因此，必须由共同安装程序将文件复制到 windows xp 系统，否则，你应该为 windows xp 提供单独的经过修饰的部分。

     

-   **USB\_安装。 HW**：此部分是 .inf 文件中的密钥。 它指定设备的设备接口全局唯一标识符（GUID）。 **AddReg**指令将指定的接口 GUID 设置为标准的注册表值。 当 Winusb 作为设备的函数驱动程序加载时，它将读取注册表值 DeviceInterfaceGUIDs 键，并使用指定的 GUID 来表示设备接口。 应将此示例中的 GUID 替换为专用于设备创建的 GUID。 如果设备的协议发生更改，请创建新的设备接口 GUID。

    **请注意**  用户模式软件必须调用[**SetupDiGetClassDevs**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw) ，以枚举与 DeviceInterfaceGUIDs 密钥下指定的某个设备接口类相关联的已注册设备接口。 **SetupDiGetClassDevs**返回设备的设备句柄，用户模式软件随后必须将其传递到[**WinUsb\_初始化**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize)例程以获取设备接口的 WinUsb 句柄。 有关这些例程的详细信息，请参阅[如何使用 WinUSB 功能访问 USB 设备](using-winusb-api-to-communicate-with-a-usb-device.md)。

以下 INF 在基于 x64 的系统上将 WinUSB 安装为 OSR USB FX2 板的函数驱动程序。 该示例显示了具有 WDF coinstallers 的 INF。

``` syntax
;
;
; Installs WinUsb
;

[Version]
Signature = "$Windows NT$"
Class     = USBDevice
ClassGUID = {88BAE032-5A81-49f0-BC3D-A4FF138216D6}
Provider  = %ManufacturerName%
CatalogFile = WinUSBInstallation.cat
DriverVer=09/04/2012,13.54.20.543

; ========== Manufacturer/Models sections ===========

[Manufacturer]
%ManufacturerName% = Standard,NTamd64

[Standard.NTamd64]
%DeviceName% =USB_Install, USB\VID_0547&PID_1002

; ========== Class definition (for Windows 8 and ealier versions) ===========

[ClassInstall32]
AddReg = ClassInstall_AddReg

[ClassInstall_AddReg]
HKR,,,,%ClassName%
HKR,,NoInstallClass,,1
HKR,,IconPath,%REG_MULTI_SZ%,"%systemroot%\system32\setupapi.dll,-20"
HKR,,LowerLogoVersion,,5.2

; =================== Installation ===================

[USB_Install]
Include = winusb.inf
Needs   = WINUSB.NT

[USB_Install.Services]
Include =winusb.inf
Needs   = WINUSB.NT.Services

[USB_Install.HW]
AddReg=Dev_AddReg

[Dev_AddReg]
HKR,,DeviceInterfaceGUIDs,0x10000,"{9f543223-cede-4fa3-b376-a25ce9a30e74}"

[USB_Install.CoInstallers]
AddReg=CoInstallers_AddReg
CopyFiles=CoInstallers_CopyFiles

[CoInstallers_AddReg]
HKR,,CoInstallers32,0x00010000,"WdfCoInstaller01011.dll,WdfCoInstaller","WinUsbCoInstaller2.dll"

[CoInstallers_CopyFiles]
WinUsbCoInstaller2.dll
WdfCoInstaller01011.dll

[DestinationDirs]
; If your INF needs to copy files, you must not use the DefaultDestDir directive here.  
CoInstallers_CopyFiles=11
; ================= Source Media Section =====================

[SourceDisksNames]
1 = %DiskName%

[SourceDisksFiles]
WinUsbCoInstaller2.dll=1
WdfCoInstaller01011.dll=1


; =================== Strings ===================

[Strings]
ManufacturerName=""
ClassName="Universal Serial Bus devices"
DeviceName="Fx2 Learning Kit Device"
DiskName="MyDisk"
REG_MULTI_SZ = 0x00010000
```

-   **USB\_CoInstallers**：此部分包含引用的**AddReg**和**CopyFiles**节，其中包含用于安装 WinUSB 和 KMDF 共同安装程序并将其与设备关联的数据和说明。 大多数 USB 设备无需修改即可使用这些部分和指令。
-   基于 x86 和 x64 的 Windows 版本具有单独的共同安装程序。

    **请注意**  每个共同安装程序都有免费和已检查的版本。 使用免费版本在 Windows 免费版本（包括所有零售版）上安装 WinUSB。 使用 checked 版本（带有 "\_.chk" 后缀）在 Windows 的已选择版本上安装 WinUSB。

每次 Winusb 加载时，它都会注册一个设备接口，该接口具有在**DeviceInterfaceGUIDs**项下的注册表中指定的设备接口类。

``` syntax
HKR,,DeviceInterfaceGUIDs, 0x10000,"{D696BFEB-1734-417d-8A04-86D01071C512}"
```

**请注意**  如果你使用适用于 windows XP 或 windows Server 2003 的可再发行 WinUSB 包，请确保不要在卸载包中卸载 WinUSB。 其他 USB 设备可能正在使用 WinUSB，因此其二进制文件必须保留在共享文件夹中。

 

## <a href="" id="howto"></a>如何创建驱动程序包以安装 Winusb


若要将 WinUSB 用作设备的函数驱动程序，请创建一个驱动程序包。 驱动程序包必须包含以下文件：

-   WinUSB 共同安装程序（Winusbcoinstaller）
-   KMDF 共同安装程序（WdfcoinstallerXXX）
-   将 Winusb 安装为设备的函数驱动程序的 .inf 文件。 有关详细信息，请参阅[编写。用于 WinUSB 安装的 Inf 文件](#inf)。
-   包的已签名的目录文件。 此文件是在 x64 版本的 Windows 上安装 WinUSB 所必需的。

![winusb 安装包](images/winusb-package.jpg)

**请注意**  确保驱动程序包内容满足以下要求：
-   必须从同一版本的 Windows 驱动程序工具包（WDK）获取 KMDF 和 WinUSB 共同安装程序文件。
-   必须从最新版本的 WDK 获取共同安装程序文件，以便驱动程序支持所有最新的 Windows 版本。
-   必须使用 Winqual 版本签名对驱动程序包的内容进行数字签名。 有关如何创建和测试签名目录文件的详细信息，请参阅 Windows 开发人员中心-硬件站点上的[内核模式代码签名演练](https://go.microsoft.com/fwlink/p/?linkid=129409)。

 

1. [下载并安装 Windows 驱动程序工具包（WDK）](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk) 。
2. 在 USB 设备连接到的计算机上创建一个驱动程序包文件夹。 例如，c：\\UsbDevice。
3. 将 WinUSB 共同安装程序（WinusbcoinstallerX）从**WinDDK\\** <em>BuildNumber</em> **\\\\WinUSB**文件夹复制到驱动程序包文件夹。

   WinUSB 安装程序（Winusbcoinstaller）在目标系统上安装 WinUSB （如有必要）。 WDK 包括三个版本的共同安装程序，具体取决于系统体系结构：基于 x86、基于 x64 和基于 Itanium 的系统。 它们都命名为 WinusbcoinstallerX，位于**WinDDK\\** <em>BuildNumber</em> **\\\\winusb**文件夹的相应子目录中。

4. 将 KMDF 共同安装程序（WdfcoinstallerXXX）从**WinDDK\\** <em>BuildNumber</em> **\\\\wdf**文件夹复制到驱动程序包文件夹。

   KMDF 共同安装程序（WdfcoinstallerXXX）在目标系统上安装正确的 KMDF 版本（如有必要）。 WinUSB 共同安装程序的版本必须与 KMDF 共同安装程序匹配，因为基于 KMDF 的客户端驱动程序（如 Winusb）要求在系统上正确安装相应版本的 KMDF framework。 例如，Winusbcoinstaller2 需要 KMDF 版本1.9，该版本由 Wdfcoinstaller01009 安装。 WdfcoinstallerXXX 的 x86 和 x64 版本包含在 WDK 下的**WinDDK\\** <em>BuildNumber</em> **\\\\wdf**文件夹中。 下表显示了要在目标系统上使用的 WinUSB 共同安装程序和关联的 KMDF 共同安装程序。

   使用此表来确定 WinUSB 共同安装程序和关联的 KMDF 共同安装程序。

   <table>
   <colgroup>
   <col width="33%" />
   <col width="33%" />
   <col width="33%" />
   </colgroup>
   <thead>
   <tr class="header">
   <th>WinUSB 共同安装程序</th>
   <th>KMDF 库版本</th>
   <th>KMDF 共同安装程序</th>
   </tr>
   </thead>
   <tbody>
   <tr class="odd">
   <td>Winusbcoinstaller</td>
   <td>需要 KMDF 版本1.5 或更高版本</td>
   <td><p>Wdfcoinstaller01005</p>
   <p>Wdfcoinstaller01007</p>
   <p>Wdfcoinstaller01009</p></td>
   </tr>
   <tr class="even">
   <td>Winusbcoinstaller2</td>
   <td>需要 KMDF 版本1.9 或更高版本</td>
   <td>Wdfcoinstaller01009</td>
   </tr>
   <tr class="odd">
   <td>Winusbcoinstaller2</td>
   <td>需要 KMDF 版本1.11 或更高版本</td>
   <td>WdfCoInstaller01011</td>
   </tr>
   </tbody>
   </table>

     

5. 编写将 Winusb 安装为 USB 设备的函数驱动程序的 .inf 文件。
6. 为包创建签名的目录文件。 在 x64 版本的 Windows 上安装 WinUSB 时需要此文件。
7. 将 USB 设备连接到计算机。
8. 打开**设备管理器**安装驱动程序。 按照**更新驱动程序软件**向导中的说明进行操作，并选择 "手动安装"。 你将需要提供驱动程序包文件夹的位置来完成安装。

## <a name="related-topics"></a>相关主题
[WinUSB 体系结构和模块](winusb-architecture.md)  
[选择用于开发 USB 客户端驱动程序的驱动程序型号](winusb-considerations.md)  
[如何使用 WinUSB 功能访问 USB 设备](using-winusb-api-to-communicate-with-a-usb-device.md)  
[WinUSB 电源管理](winusb-power-management.md)  
[用于修改管道策略的 WinUSB 函数](winusb-functions-for-pipe-policy-modification.md)  
[WinUSB 函数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)  
[WinUSB](winusb.md)  



