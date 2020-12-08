---
title: 在使用单个 PDO 的 MFP 中安装扫描功能
description: 在使用单个 PDO 的 MFP 中安装扫描功能
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d239e549666edc75ab1889ec2e2ec413141bc6cf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813757"
---
# <a name="installing-scanning-functionality-in-an-mfp-with-a-single-pdo"></a>在使用单个 PDO 的 MFP 中安装扫描功能





在仅具有单个物理设备对象 (PDO) 的多功能打印机中安装扫描功能时，需要特殊的过程。 如果设备将自身标识为打印机，则打印机的 INF 文件可以调用 WIA 共同安装程序以安装扫描功能。

Microsoft 建议多功能打印机的每个逻辑功能都应有自己的 PDO （如果可能）。 应避免使用单个 PDO 关联设备的多个功能。

如果将 WIA 共同安装程序注册为设备的共同安装程序，则安装程序将始终调用 WIA 共同安装程序，以便在打印机类安装程序之前和之后处理安装。 WIA 共同安装程序会在打印机的 PDO 上创建一个 Image 类设备接口，并将所有所需的信息存储在设备接口注册表项中。 此项在注册表中的当前位置为：

**HKLM \\ SYSTEM \\ CurrentControlSet \\ Control \\ DeviceClasses \\ {6bdd1fc6-810f-11d0-bec7-08002be2092f} \\ &lt; *设备符号链接*&gt;**

在将来的操作系统版本中，不保证此密钥保留在此位置。 若要打开此密钥，请调用 [**SetupDiOpenDeviceInterfaceRegKey**](/windows/win32/api/setupapi/nf-setupapi-setupdiopendeviceinterfaceregkey)。

WIA 服务枚举所有 Image 类 PDOs 和设备接口。 因此，新创建的设备接口将被枚举为 WIA 设备。

Windows DDK 附带了一个示例 INF，它在只有一个 PDO 的多功能打印机中安装扫描功能。 此文件的名称为 *mfpoemprn*，它位于 *\\ src \\ print \\ inf* 目录中。

**在 MFP 中安装扫描功能**

1.  1. 将 *sti \_ci.dll* 指定为 **CoInstallerEntry** 条目的条目值。

    设备的 INF 必须具有 [**Inf DDInstall. CoInstallers 部分**](../install/inf-ddinstall-coinstallers-section.md) ，才能注册设备安装的共同安装程序。 此部分应如下所示：

    ```INF
    [OEMMFP.GPD.CoInstallers]
    AddReg=WIA.CoInstallers.AddReg

    [WIA.CoInstallers.AddReg]
    HKR,,CoInstallers32,0x00010000,"sti_ci.dll, CoInstallerEntry"
    ```

2.  2. 在 [**INF DDInstall 部分**](../install/inf-ddinstall-section.md)中包含 **WIASection** 条目，该条目引用包含所有 WIA 相关设置的部分。 包含 WIA 相关设置的部分必须出现在同一个 INF 文件中。

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

    通过包含 **WIASection** 项，Image 类安装程序不会为设备创建 devnode，而是创建其他设备接口。 因此，它使用前面提到的设备接口注册表项来存储 STI-/WIA-related 信息。

3.  3. 确保 [**INF DDInstall 部分**](../install/inf-ddinstall-section.md) 复制所有必需的文件。

    或者，可以列出要在 **WIASection** 中复制的文件，但不会在设备管理器中列出这些文件。

**注意**  在 **WIASection** 节中无法使用 "**包括**" 和 "**需要**" 条目。
所有内核模式部分必须由原始 [**INF DDInstall 部分**](../install/inf-ddinstall-section.md)安装。

如果设备是热插拔设备，并且需要其自己的内核模式组件，则它必须创建并启用 Image 类设备接口 (以及任何其他类设备接口（如 Print class 设备接口) 。 内核模式组件通过调用 [**IoSetDeviceInterfaceState**](/windows-hardware/drivers/ddi/wdm/nf-wdm-iosetdeviceinterfacestate) 函数在设备的 devnode 上启用 Image 类设备接口。 启用 Image 类设备接口后，将触发即插即用事件，并通知 WIA 服务设备已连接。

 

 

