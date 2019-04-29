---
Description: 在内核模式堆栈中设备的 USB 设备的功能而不是实现一个驱动程序的驱动程序作为安装 WinUSB (Winusb.sys)。
title: WinUSB (Winusb.sys) 安装
ms.date: 05/09/2018
ms.localizationpriority: medium
ms.openlocfilehash: 0898e03722bfa73103966b5855cc016d9ce05ef1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389178"
---
# <a name="winusb-winusbsys-installation"></a>WinUSB (Winusb.sys) 安装


对于某些通用串行总线 (USB) 设备，如仅单个应用程序，访问的设备，你可以安装[WinUSB](winusb.md) (Winusb.sys) 设备的 USB 设备的功能驱动程序，而不是作为内核模式堆栈中实现一个驱动程序。

本主题包含以下部分：

-   [自动安装 WinUSB 没有 INF 文件](#automatic-installation-of--winusb-without-an-inf-file)
-   [通过指定的系统提供的设备类安装 WinUSB](#installing-winusb-by-specifying--the-system-provided-device-class)
-   [编写 WinUSB 安装自定义 INF](#inf)
-   [如何创建驱动程序包安装 Winusb.sys](#howto)

## <a href="" id="automatic-installation-of--winusb-without-an-inf-file"></a>自动安装 WinUSB 没有 INF 文件


作为 OEM 或独立硬件供应商 (IHV)，您可以构建你的设备，以便 Winusb.sys 获取 Windows 8 和更高版本的操作系统上自动安装。 此类设备称为 WinUSB 设备，不需要你编写自定义引用现成 Winusb.inf INF 文件。

WinUSB 设备连接时，系统将读取设备信息，并自动加载 Winusb.sys。

有关详细信息，请参阅[WinUSB 设备](automatic-installation-of-winusb.md)。

## <a href="" id="installing-winusb-by-specifying--the-system-provided-device-class"></a>通过指定的系统提供的设备类安装 WinUSB


当连接你的设备时，您可能注意到，Windows 加载 Winusb.sys 自动 （是否 IHV 已定义为 WinUSB 设备的设备）。 否则，请按照这些说明来加载该驱动程序：

1.  插入您的设备与主机系统。
2.  打开设备管理器，找到该设备。
3.  右键单击该设备，然后选择**更新驱动程序软件...** 从上下文菜单。
4.  在向导中，选择**浏览计算机以查找驱动程序软件**。
5.  选择**让我在我的计算机上从设备驱动程序的列表中选取**。
6.  从设备类的列表中选择**通用串行总线设备**。
7.  该向导将显示**WinUsb 设备**。 选择它以加载该驱动程序。

如果**通用串行总线设备**中没有的设备类的列表，则需要使用自定义 INF 安装驱动程序。
在前面的过程不会添加的应用 （UWP 应用或 Windows 桌面应用程序） 来访问设备的设备接口的 GUID。 按照以下步骤，必须手动添加 GUID。

1.  加载驱动程序，如前面的过程中所述。
2.  通过使用 guidgen.exe 之类的工具生成你的设备，设备接口的 GUID。
3.  找到此项下设备的注册表项：

    **HKEY\_LOCAL\_MACHINE\\SYSTEM\\CurrentControlSet\\Enum\\USB\\&lt;VID\_vvvv&PID\_pppp&gt;**

4.  下**设备参数**密钥，请添加名为一个字符串注册表项**DeviceInterfaceGUID**或名为多字符串条目**DeviceInterfaceGUIDs**。 将值设置为在步骤 2 中生成的 GUID。
5.  从系统中断开设备并将其重新连接到同一个物理端口。
    **请注意**  如果更改的物理端口，则必须重复步骤 1 至 4。

     

## <a href="" id="inf"></a>编写 WinUSB 安装自定义 INF


驱动程序包的一部分，为您提供将 Winusb.sys 作为 USB 设备的功能驱动程序安装的.inf 文件。

下面的.inf 文件示例演示了一些修改，如更改大多数 USB 设备的 WinUSB 安装**USB\_安装**中对相应的节名称*DDInstall*值。 此外应更改版本、 制造商和根据需要的模型部分。 例如，为设备提供相应制造商的名称、 签名的编录文件中，正确的设备类，以及供应商标识符 (VID) 和产品标识符 (PID) 的名称。

另请注意，安装程序类设置为"USBDevice"。 对于不属于另一个类并不是 USB 主控制器或中心的设备，供应商可以使用"USBDevice"安装程序类。

如果您正在安装 WinUSB 作为 USB 复合设备中的函数之一的函数驱动程序，必须提供与中 INF 的函数相关联的硬件 ID。 可以从在 devnode 属性获取该函数的硬件 ID**设备管理器**。 硬件 ID 字符串格式是"USB\\VID\_vvvv & PID\_pppp"。

以下 INF 安装 WinUSB 作为 OSR USB FX2 板的功能的基于 x64 的系统上的驱动程序。

> 从 Windows 10，版本 1709，开始 Windows 驱动程序工具包提供了[InfVerif.exe](https://docs.microsoft.com/windows-hardware/drivers/devtest/infverif)可用于测试以确保没有任何语法问题和 INF 文件是通用的驱动程序 INF 文件。 我们建议您提供通用 INF。 有关详细信息，请参阅[使用通用 INF 文件](https://docs.microsoft.com/windows-hardware/drivers/install/using-a-universal-inf-file)。

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
> 仅在要安装新的自定义设备安装程序类的设备 INF 文件中包含的 ClassInstall32 部分。 在已安装类中，设备的 INF 文件还是系统提供的设备安装程序类的自定义类，不能包含 ClassInstall32 部分。 




除了特定于设备的值和下面的列表中所述的几个问题，可以使用这些部分和指令 WinUSB 安装任何 USB 设备。 这些列表各项介绍了**包括**并**指令**前面的.inf 文件中。

-   **USB\_安装**:**Include**并**需要**中的指令**USB\_安装**部分所需的安装 WinUSB。 不应修改这些指令。
-   **USB\_Install.Services**:**Include**指令**USB\_Install.Services**部分包括有关 WinUSB (WinUSB.inf) 系统提供的.inf。 如果尚未在目标系统上，WinUSB 共同安装程序被安装此.inf 文件。 **需要**指令指定包含安装 Winusb.sys 作为设备的功能驱动程序所需的信息的 WinUSB.inf 内的部分。 不应修改这些指令。
    **请注意**  因为 Windows XP 不提供 WinUSB.inf、 必须要么将文件复制到 Windows XP 系统共同安装程序，或应为 Windows XP 提供单独的修饰的部分。

     

-   **USB\_Install.HW**:本部分是.inf 文件中的密钥。 它指定的设备接口全局唯一标识符 (GUID) 为你的设备。 **AddReg**指令设置标准注册表值中的指定的接口的 GUID。 Winusb.sys 作为设备的功能驱动程序加载时，它将读取注册表值 DeviceInterfaceGUIDs 项并使用指定的 GUID 来表示设备接口。 您应该使用专门针对你的设备创建来替换在此示例中的 GUID。 如果更改设备的协议，请创建一个新的设备接口的 GUID。

    **请注意**  用户模式软件必须调用[ **SetupDiGetClassDevs** ](https://msdn.microsoft.com/library/windows/hardware/ff551069)来枚举与设备接口之一相关联的已注册的设备接口DeviceInterfaceGUIDs 项下指定的类。 **SetupDiGetClassDevs**返回用户模式软件必须传递到设备的设备句柄[ **WinUsb\_初始化**](https://msdn.microsoft.com/library/windows/hardware/ff540277)例程，以获取 WinUSB 句柄设备接口。 有关这些例程的详细信息，请参阅[如何访问由使用 WinUSB 函数 USB 设备](using-winusb-api-to-communicate-with-a-usb-device.md)。

以下 INF 安装 WinUSB 作为 OSR USB FX2 板的功能的基于 x64 的系统上的驱动程序。 示例演示了 WDF 共同安装程序的 INF。

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

-   **USB\_Install.CoInstallers**:本部分中，其中包括被引用**AddReg**并**CopyFiles**部分时，包含数据和说明来安装 WinUSB 和 KMDF 共同安装程序并将其与设备关联。 大多数 USB 设备可以使用这些部分和无需修改的指令。
-   Windows 的基于 x86 和基于 x64 的版本具有不同的共同安装程序。

    **请注意**  每个共同安装程序没有选中免费版。 使用免费版本的 Windows，包括所有的零售版本的免费版本上安装 WinUSB。 使用经检查的版本 (与"\_chk"后缀) 上检查内部版本号的 Windows 安装 WinUSB。

每次 Winusb.sys 加载时，它会注册其设备界面包含注册表中指定的设备接口类**DeviceInterfaceGUIDs**密钥。

``` syntax
HKR,,DeviceInterfaceGUIDs, 0x10000,"{D696BFEB-1734-417d-8A04-86D01071C512}"
```

**请注意**  如果可再发行组件 WinUSB 包用于 Windows XP 或 Windows Server 2003，请确保在卸载包中不卸载 WinUSB。 其他 USB 设备可能会使用 WinUSB，因此其二进制文件必须保留在共享文件夹中。

 

## <a href="" id="howto"></a>如何创建驱动程序包安装 Winusb.sys


若要使用 WinUSB 作为设备的功能驱动程序，您创建驱动程序包。 驱动程序包必须包含这些文件：

-   WinUSB 共同安装程序 (Winusbcoinstaller.dll)
-   KMDF 共同安装程序 (WdfcoinstallerXXX.dll)
-   安装 Winusb.sys 作为设备的功能驱动程序.inf 文件。 有关详细信息，请参阅[写入。Inf 文件 WinUSB 安装](#inf)。
-   包签名的编录文件。 在 x64 上安装 WinUSB 所需的此文件版本的 Windows Vista 从开始。

![winusb 安装包](images/winusb-package.jpg)

**请注意**  确保驱动程序程序包的内容符合这些要求：
-   必须从相同版本的 Windows Driver Kit (WDK) 获取 KMDF 和 WinUSB 共同安装程序文件。
-   必须从最新版本的 wdk 获取共同安装程序文件，以便该驱动程序支持所有最新的 Windows 版本。
-   驱动程序包的内容必须使用 Winqual 版本签名中进行数字签名。 有关如何创建和测试签名的编录文件的详细信息，请参阅[内核模式代码签名演练](https://go.microsoft.com/fwlink/p/?linkid=129409)Windows 开发人员中心-硬件站点上。

 

1. [下载 Windows Driver Kit (WDK)](https://docs.microsoft.com/windows-hardware/drivers/download-the-wdk)并将其安装。
2. USB 设备连接到计算机上创建驱动程序包文件夹。 例如，c:\\UsbDevice。
3. 从复制 WinUSB 共同安装程序 (WinusbcoinstallerX.dll) **WinDDK\\**<em>BuildNumber</em>**\\redist\\winusb**驱动程序的包文件夹的文件夹。

   如有必要，WinUSB 共同安装程序 (Winusbcoinstaller.dll) 目标系统上安装 WinUSB。 WDK 包括具体取决于系统体系结构的共同安装程序的三个版本： 基于 x86 的、 基于 x64 和基于 Itanium 的系统。 它们都命名为 WinusbcoinstallerX.dll，位于中的相应子目录**WinDDK\\**<em>BuildNumber</em>**\\redist\\winusb**文件夹。

4. 从复制 KMDF 共同安装程序 (WdfcoinstallerXXX.dll) **WinDDK\\**<em>BuildNumber</em>**\\redist\\wdf**到文件夹驱动程序包文件夹中。

   如有必要，KMDF 共同安装程序 (WdfcoinstallerXXX.dll) 目标系统上安装正确版本的 KMDF。 WinUSB 共同安装程序的版本必须与匹配 KMDF 共同安装程序，因为 KMDF 基于客户端驱动程序，例如 Winusb.sys，需要在系统上正确安装 KMDF framework 的相应版本。 例如，Winusbcoinstaller2.dll 需要 KMDF 1.9 版，Wdfcoinstaller01009.dll 安装。 WdfcoinstallerXXX.dll 的 x86 和 x64 版本所含下 WDK **WinDDK\\**<em>BuildNumber</em>**\\redist\\wdf**文件夹。 下表显示了 WinUSB 共同安装程序和关联的 KMDF 共同安装程序为目标系统上使用。

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
   <td>Winusbcoinstaller.dll</td>
   <td>需要 KMDF 1.5 或更高版本</td>
   <td><p>Wdfcoinstaller01005.dll</p>
   <p>Wdfcoinstaller01007.dll</p>
   <p>Wdfcoinstaller01009.dll</p></td>
   </tr>
   <tr class="even">
   <td>Winusbcoinstaller2.dll</td>
   <td>需要 KMDF 1.9 或更高版本</td>
   <td>Wdfcoinstaller01009.dll</td>
   </tr>
   <tr class="odd">
   <td>Winusbcoinstaller2.dll</td>
   <td>需要 KMDF 版本 1.11 或更高版本</td>
   <td>WdfCoInstaller01011.dll</td>
   </tr>
   </tbody>
   </table>

     

5. 编写将 Winusb.sys 作为 USB 设备的功能驱动程序安装的.inf 文件。
6. 创建签名的编录文件的包。 在 x64 上安装 WinUSB 所需的此文件的 Windows 版本。
7. USB 设备连接到您的计算机。
8. 打开**设备管理器**安装驱动程序。 按照上的说明**更新驱动程序软件**向导并选择手动安装。 需要提供包文件夹，以完成安装的驱动程序的位置。

## <a name="related-topics"></a>相关主题
[WinUSB 体系结构和模块](winusb-architecture.md)  
[选择用于开发 USB 客户端驱动程序的驱动程序模型](winusb-considerations.md)  
[如何通过使用 WinUSB 函数访问 USB 设备](using-winusb-api-to-communicate-with-a-usb-device.md)  
[WinUSB 电源管理](winusb-power-management.md)  
[针对管道策略修改 WinUSB 函数](winusb-functions-for-pipe-policy-modification.md)  
[WinUSB 函数](https://msdn.microsoft.com/library/windows/hardware/ff540046#winusb)  
[WinUSB](winusb.md)  



