---
description: 将 WinUSB (Winusb.sys) 安装在设备的内核模式堆栈中，将其作为 USB 设备的功能驱动程序，而不是实现驱动程序。
title: WinUSB (Winusb.sys) 安装
ms.date: 05/09/2018
ms.localizationpriority: High
ms.openlocfilehash: a3586830cde7cd720e92603e071099d018cfe533
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969386"
---
# <a name="winusb-winusbsys-installation"></a>WinUSB (Winusb.sys) 安装


对于某些通用串行总线 (USB) 设备（例如只能通过单个应用程序访问的设备），你可以在设备的内核模式堆栈中安装 [WinUSB](winusb.md) (Winusb.sys)，将其作为 USB 设备的功能驱动程序，而不是实现驱动程序。

本主题包含以下部分：

-   [不使用 INF 文件自动安装 WinUSB](#automatic-installation-of--winusb-without-an-inf-file)
-   [通过指定系统提供的设备类别来安装 WinUSB](#installing-winusb-by-specifying--the-system-provided-device-class)
-   [编写用于 WinUSB 安装的自定义 INF](#inf)
-   [如何创建安装 Winusb.sys 的驱动程序包](#howto)

## <a name="automatic-installation-of-winusb-without-an-inf-file"></a><a href="" id="automatic-installation-of--winusb-without-an-inf-file"></a>不使用 INF 文件自动安装 WinUSB


OEM 或独立硬件供应商 (IHV) 可以构建设备，以便在 Windows 8 及更高版本的操作系统上自动安装 Winusb.sys。 此类设备称为 WinUSB 设备，无需编写引用内置 Winusb.inf 的自定义 INF 文件。

连接 WinUSB 设备时，系统自动读取设备信息并加载 Winusb.sys。

有关详细信息，请参阅 [WinUSB 设备](automatic-installation-of-winusb.md)。

## <a name="installing-winusb-by-specifying-the-system-provided-device-class"></a><a href="" id="installing-winusb-by-specifying--the-system-provided-device-class"></a>通过指定系统提供的设备类别来安装 WinUSB


连接设备时，你可能会注意到 Windows 自动加载 Winusb.sys（如果 IHV 已将设备定义为 WinUSB 设备）。 否则，请按照以下说明加载驱动程序：

1.  将设备插入主机系统。
2.  打开设备管理器并找到设备。
3.  右键单击设备，然后从上下文菜单中选择“更新驱动程序软件…”  。
4.  在向导中，选择“浏览我的计算机以查找驱动程序软件”  。
5.  选择“从计算机的设备驱动程序列表中选择”  。
6.  从设备类别的列表中，选择“通用串行总线设备”  。
7.  向导显示“WinUsb 设备”  。 选择此项以加载驱动程序。

如果“通用串行总线设备”没有出现在设备类别列表中，则需要使用自定义 INF 安装驱动程序  。
前面的过程并没有为应用（UWP 应用或 Windows 桌面应用）添加访问设备的设备接口 GUID。 必须按照此过程手动添加 GUID。

1.  按照上述过程中的说明加载驱动程序。
2.  使用 guidgen.exe 等工具生成设备的设备接口 GUID。
3.  在此项下找到设备的注册表项：

    HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Enum\\USB\\&lt;VID\_vvvv&PID\_pppp&gt; 

4.  在“设备参数”项下，添加名为“DeviceInterfaceGUID”的字符串注册表项或名为“DeviceInterfaceGUIDs”的多字符串项    。 将值设置为你在步骤 2 中生成的 GUID。
5.  断开设备与系统的连接，然后将其重新连接到同一个物理端口。
    **注意**  如果更改物理端口，则必须重复步骤 1 到步骤 4。

     

## <a name="writing-a-custom-inf-for-winusb-installation"></a><a href="" id="inf"></a>编写用于 WinUSB 安装的自定义 INF


驱动程序包中有一个 .inf 文件，该文件可将 Winusb.sys 安装为 USB 设备的功能驱动程序。

以下示例 .inf 文件显示了对大多数 USB 设备的 WinUSB 安装，并进行了一些修改，例如将节名称中的 USB\_Install 更改为适当的 DDInstall 值   。 还应根据需要更改版本、制造商和型号部分。 例如，提供适当的制造商的名称、签名的目录文件的名称、正确的设备类别以及设备的供应商标识符 (VID) 和产品标识符 (PID)。

另请注意，安装程序类设置为“USBDevice”。 对于不属于其他类且不是 USB 主机控制器或集线器的设备，供应商可以使用“USBDevice”安装程序类。

如果要将 WinUSB 安装为 USB 复合设备中某个功能的功能驱动程序，则必须在 INF 中提供与该功能关联的硬件 ID。 可以从“设备管理器”中的 devnode 的属性获取该功能的硬件 ID  。 硬件 ID 字符串格式为“USB\\VID\_vvvv&PID\_pppp”。

以下 INF 在基于 x64 的系统上将 WinUSB 安装为 OSR USB FX2 板的功能驱动程序。

> 从 Windows 10 1709 版开始，Windows 驱动程序工具包提供 [InfVerif.exe](https://docs.microsoft.com/windows-hardware/drivers/devtest/infverif)，你可以使用它来测试驱动程序 INF 文件，以确保没有语法问题并且 INF 文件是通用的。 建议提供通用 INF。 有关详细信息，请参阅[使用通用 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/using-a-universal-inf-file)。

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
> 仅在设备 INF 文件中包含 ClassInstall32 部分，以安装新的自定义设备安装程序类。 已安装类中的设备的 INF 文件（无论系统提供的是设备安装程序类还是自定义类）都不能包含 ClassInstall32 部分。 




除特定于设备的值以及以下列表中所述的几个问题之外，还可以使用这些部分和指令来安装适用于任何 USB 设备的 WinUSB。 这些列表项描述了上述 .inf 文件中的 Includes 和 Directives   。

-   **USB\_Install**：安装 WinUSB 需要 USB\_Install 部分中的 Include 和 Needs 指令    。 不应修改这些指令。
-   **USB\_Install.Services**：USB\_Install.Services 部分中的 Include 指令包括用于 WinUSB (WinUSB.inf) 的系统提供的 .inf   。 如果目标系统上尚未安装此 .inf 文件，则该文件由 WinUSB 辅助安装程序安装。 Needs 指令指定 WinUSB.inf 中的部分，其中包含将 Winusb.sys 安装为设备的功能驱动程序所需的信息  。 不应修改这些指令。
    **注意**  由于 Windows XP 不提供 WinUSB.inf，因此，必须由辅助安装程序将文件复制到 Windows XP 系统；否则，你应为 Windows XP 提供单独的经过修饰的部分。

     

-   **USB\_Install.HW**：本部分是 .inf 文件中的项。 它指定设备的设备接口全局唯一标识符 (GUID)。 AddReg 指令在标准注册表值中设置指定的接口 GUID  。 当 Winusb.sys 作为设备的功能驱动程序加载时，它将读取注册表值 DeviceInterfaceGUIDs 项，并使用指定的 GUID 来表示设备接口。 在此示例中，应将 GUID 替换为专门为设备创建的 GUID。 如果设备的协议发生更改，请创建新的设备接口 GUID。

    **注意**  用户模式软件必须调用 [SetupDiGetClassDevs](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdigetclassdevsw) 才能枚举与在 DeviceInterfaceGUIDs 项下指定的某个设备接口类关联的已注册设备接口  。 SetupDiGetClassDevs 返回了设备的设备句柄，然后用户模式软件必须将设备句柄传递给 [WinUsb\_Initialize](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_initialize) 例程，以获取设备接口的 WinUSB 句柄   。 有关这些例程的详细信息，请参阅[如何使用 WinUSB Functions 访问 USB 设备](using-winusb-api-to-communicate-with-a-usb-device.md)。

以下 INF 在基于 x64 的系统上将 WinUSB 安装为 OSR USB FX2 板的功能驱动程序。 该示例显示了 WDF 辅助安装程序的 INF。

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

-   **USB\_Install.CoInstallers**：本部分（包括引用的 AddReg 和 CopyFiles 部分）包含用于安装 WinUSB 和 KMDF 辅助安装程序并将其与设备关联的数据和说明   。 大多数 USB 设备无需修改即可使用这些部分和指令。
-   Windows 基于 x86 和基于 x64 的版本具有单独的辅助安装程序。

    **注意**  每个辅助安装程序都有免费版本和经过检查的版本。 使用免费版本可在 Windows 免费版本（包括所有零售版）上安装 WinUSB。 使用经过检查的版本（带有“\_chk”后缀）在经过检查的 Windows 版本上安装 WinUSB。

每次 Winusb.sys 加载时，它都会注册一个设备接口，该设备接口具有在 DeviceInterfaceGUIDs 项下的注册表中指定的设备接口类  。

``` syntax
HKR,,DeviceInterfaceGUIDs, 0x10000,"{D696BFEB-1734-417d-8A04-86D01071C512}"
```

**注意**  如果使用适用于 Windows XP 或 Windows Server 2003 的可再发行 WinUSB 包，请确保不要在卸载包中卸载 WinUSB。 其他 USB 设备可能正在使用 WinUSB，因此其二进制文件必须保留在共享文件夹中。

 

## <a name="how-to-create-a-driver-package-that-installs-winusbsys"></a><a href="" id="howto"></a>如何创建安装 Winusb.sys 的驱动程序包


若要将 WinUSB 用作设备的功能驱动程序，请创建一个驱动程序包。 驱动程序包必须包含以下文件：

-   WinUSB 辅助安装程序 (Winusbcoinstaller.dll)
-   KMDF 辅助安装程序 (WdfcoinstallerXXX.dll)
-   一个 .inf 文件，用于将 Winusb.sys 安装为设备的功能驱动程序。 有关详细信息，请参阅[编写用于 WinUSB 安装的 Inf 文件](#inf)。
-   包的已签名目录文件。 从 Vista 开始，在 Windows x64 版本上安装 WinUSB 时需要此文件。

![winusb 安装包](images/winusb-package.jpg)

**注意**  确保驱动程序包内容满足以下要求：
-   必须从相同版本的 Windows 驱动程序工具包 (WDK) 获取 KMDF 和 WinUSB 辅助安装程序文件。
-   必须从最新版本的 WDK 获取辅助安装程序文件，以便驱动程序支持所有最新的 Windows 版本。
-   必须使用 Winqual 版本签名对驱动程序包的内容进行数字签名。 有关如何创建和测试已签名的目录文件的详细信息，请参阅 Windows 开发人员中心硬件站点上的[内核模式代码签名演练](https://go.microsoft.com/fwlink/p/?linkid=129409)。

 

1. [下载 Windows 驱动程序工具包 (WDK)](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk) 并安装此包。
2. 在连接 USB 设备的计算机上创建驱动程序包文件夹。 例如，c:\\UsbDevice。
3. 将 WinUSB 辅助安装程序 (WinusbcoinstallerX.dll) 从 WinDDK\\<em>BuildNumber</em>\\redist\\winusb 文件夹复制到驱动程序包文件夹   。

   WinUSB 辅助安装程序 (Winusbcoinstaller.dll) 根据需要在目标系统上安装 WinUSB。 WDK 包括三个版本的辅助安装程序，具体取决于以下系统体系结构：基于 x86 的系统、基于 x64 的系统和基于 Itanium 的系统。 它们都命名为 WinusbcoinstallerX，并且位于 WinDDK\\<em>BuildNumber</em>\\redist\\winusb 文件夹的相应子目录中   。

4. 将 KMDF 辅助安装程序 (WdfcoinstallerXXX.dll) 从 WinDDK\\<em>BuildNumber</em>\\redist\\wdf 文件夹复制到驱动程序包文件夹   。

   KMDF 辅助安装程序 (WdfcoinstallerXXX.dll) 根据需要在目标系统上安装适当的 KMDF 版本。 WinUSB 辅助安装程序的版本必须与 KMDF 辅助安装程序匹配，因为基于 KMDF 的客户端驱动程序（例如 Winusb.sys）要求在系统上正确安装相应版本的 KMDF 框架。 例如，Winusbcoinstaller2 需要 KMDF 版本1.9，该版本由 Wdfcoinstaller01009 安装。 WdfcoinstallerXXX 的 x86 和 x64 版本都包含在 WinDDK\\<em>BuildNumber</em>\\redist\\wdf 文件夹下的 WDK 中   。 下表显示了要在目标系统上使用的 WinUSB 辅助安装程序和关联的 KMDF 辅助安装程序。

   使用此表可确定 WinUSB 辅助安装程序和关联的 KMDF 辅助安装程序。

   <table>
   <colgroup>
   <col width="33%" />
   <col width="33%" />
   <col width="33%" />
   </colgroup>
   <thead>
   <tr class="header">
   <th>WinUSB 辅助安装程序</th>
   <th>KMDF 库版本</th>
   <th>KMDF 辅助安装程序</th>
   </tr>
   </thead>
   <tbody>
   <tr class="odd">
   <td>Winusbcoinstaller.dll</td>
   <td>需要 KMDF 版本 1.5 或更高版本</td>
   <td><p>Wdfcoinstaller01005.dll</p>
   <p>Wdfcoinstaller01007.dll</p>
   <p>Wdfcoinstaller01009.dll</p></td>
   </tr>
   <tr class="even">
   <td>Winusbcoinstaller2.dll</td>
   <td>需要 KMDF 版本 1.9 或更高版本</td>
   <td>Wdfcoinstaller01009.dll</td>
   </tr>
   <tr class="odd">
   <td>Winusbcoinstaller2.dll</td>
   <td>需要 KMDF 版本 1.11 或更高版本</td>
   <td>WdfCoInstaller01011.dll</td>
   </tr>
   </tbody>
   </table>

     

5. 编写一个 .inf 文件，用于将 Winusb.sys 安装为 USB 设备的功能驱动程序。
6. 创建包的已签名目录文件。 在 Windows x64 版本上安装 WinUSB 时需要此文件。
7. 将 USB 设备连接到计算机。
8. 打开“设备管理器”，以安装驱动程序  。 按照“更新驱动程序软件”向导中的说明进行操作，然后选择手动安装  。 你需要提供驱动程序包文件夹的位置才能完成安装。

## <a name="related-topics"></a>相关主题
[WinUSB 体系结构和模块](winusb-architecture.md)  
[选择用于开发 USB 客户端驱动程序的驱动程序模型](winusb-considerations.md)  
[如何通过 WinUSB Functions 访问 USB 设备](using-winusb-api-to-communicate-with-a-usb-device.md)  
[WinUSB 电源管理](winusb-power-management.md)  
[用于修改管道策略的 WinUSB 函数](winusb-functions-for-pipe-policy-modification.md)  
[WinUSB 函数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)  
[WinUSB](winusb.md)  



