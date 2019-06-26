---
title: 在使用单个 PDO 的 MFP 中安装扫描功能
description: 在使用单个 PDO 的 MFP 中安装扫描功能
ms.assetid: 002ff319-42f9-4034-9bdd-c1e771ed2ba9
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e67482d63294d2822d114e011d70b343b2c33678
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378919"
---
# <a name="installing-scanning-functionality-in-an-mfp-with-a-single-pdo"></a>在使用单个 PDO 的 MFP 中安装扫描功能





在具有只有一个物理设备对象 (PDO) 的多功能打印机安装扫描功能需要特殊的过程。 如果该设备将自身标识为打印机，打印机的 INF 文件可以调用 WIA 共同安装程序，以便安装扫描功能。

Microsoft 建议多功能打印机的每个逻辑函数应具有其自己的 PDO，如有可能。 应避免将设备的多个函数与单个 PDO 相关联。

如果你的设备的共同安装程序作为注册 WIA 共同安装程序，安装程序将始终调用 WIA 共同安装程序来处理之前和之后的打印机类安装程序安装。 WIA 共同安装程序上打印机的 PDO 创建图像类设备接口，并将所需的所有信息都存储在设备接口注册表项。 在注册表中的此项当前的位置是：

**HKLM\\SYSTEM\\CurrentControlSet\\Control\\DeviceClasses\\{6bdd1fc6-810f-11d0-bec7-08002be2092f}\\&lt;*device symbolic link*&gt;**

此密钥不保证保留在此位置在将来的操作系统版本。 若要打开此密钥，请调用[ **SetupDiOpenDeviceInterfaceRegKey**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendeviceinterfaceregkey)。

WIA 枚举所有图像类 PDOs 和设备接口。 因此，新创建的设备接口将枚举为 WIA 的设备。

Windows DDK 附带了一个示例将扫描功能安装在具有只有一个单一的 PDO 的多功能打印机的 INF。 此文件的名称是*mfpoemprn.inf*，并且它位于 *\\src\\打印\\inf*目录。

**若要在 MFP 中安装扫描功能**

1.  1.指定*sti\_ci.dll*的项值作为**CoInstallerEntry**条目。

    必须为你的设备 INF [ **INF DDInstall.CoInstallers 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-coinstallers-section)能够注册设备安装的共同安装程序。 本部分中应显示类似于下面：

    ```INF
    [OEMMFP.GPD.CoInstallers]
    AddReg=WIA.CoInstallers.AddReg

    [WIA.CoInstallers.AddReg]
    HKR,,CoInstallers32,0x00010000,"sti_ci.dll, CoInstallerEntry"
    ```

2.  2.包括**WIASection**中的条目[ **INF DDInstall 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section) ，指的是包含所有与 WIA 相关的设置的节。 部分，其中包含与 WIA 相关的设置必须出现在同一个 INF 文件。

    ```INF
    [OEMMFP.GPD]
    CopyFiles=@OEMMFP.DLL,@OEMPRT1.DLL,@OEMUI.DLL,OEMMFP.GPD.WIA.CopyFiles
    WIASection=OEMMFP.GPD.WIA

    [OEMMFP.GPD.WIA]
    Description=%OEM_MFP_SCANNER%
    SubClass=StillImage
    DeviceType=1
    Capabilities=0x00000011
    AddReg=OEMMFP.GPD.WIA.AddReg
    DeviceData=OEMMFP.GPD.WIA.DeviceData
    ICMProfiles="sRGB Color Space Profile.icm"
    USDClass="{XXXXXXXX-XXXX-XXXX-XXXX-XXXXXXXXXXXX}"
    ```

    通过包括**WIASection**注册表项，图像类安装程序不会创建该设备，devnode 但改为创建的其他设备接口。 相应地，它使用前面所述的设备接口注册表项来存储 STI-/ WIA 相关信息。

3.  3.请确保[ **INF DDInstall 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)复制所需的所有文件。

    或者，可以列出要在复制的文件**WIASection**，但它们不会列出在设备管理器。

**请注意**   **Include**并**需要**条目不能用于**WIASection**部分。
所有内核模式部分必须都安装由原始[ **INF DDInstall 部分**](https://docs.microsoft.com/windows-hardware/drivers/install/inf-ddinstall-section)。

如果设备是热插拔，并且需要其自己的内核模式组件，它必须创建并启用图像类设备接口 （除了任何其他类设备接口，如打印类设备接口）。 内核模式组件通过调用启用图像类设备接口上设备的 devnode [ **IoSetDeviceInterfaceState** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-iosetdeviceinterfacestate)函数。 启用映像类设备接口后，会触发插事件，通知 WIA 服务设备已连接。

 

 

 




