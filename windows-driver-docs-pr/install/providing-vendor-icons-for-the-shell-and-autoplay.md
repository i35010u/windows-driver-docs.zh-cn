---
title: 为 Shell 和自动播放提供供应商图标
description: 为 Shell 和自动播放提供供应商图标
ms.assetid: 2e3afbf6-57f6-4b83-b10a-c33d9b1c1731
keywords:
- 自动播放图标 WDK
- 自定义图标 WDK 设备安装
- 供应商图标 WDK
- 图标 WDK Shell
- Shell 图标 WDK
- 媒体插入的图标 WDK
- 无媒体插入图标 WDK
- 图标 WDK 自动播放
- 复制图标文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d7fd17e7b5b1d062c68ce3e1a1c1be433ba77376
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837378"
---
# <a name="providing-vendor-icons-for-the-shell-and-autoplay"></a>为 Shell 和自动播放提供供应商图标





[自动播放](https://go.microsoft.com/fwlink/p/?linkid=12031)是 Shell 的扩展，由 MICROSOFT windows XP 和更高版本的 windows 支持。 自动播放在可移动媒体或可移动设备上检测不同类型的内容，例如音频或视频文件。 自动播放可以显示内容和设备的自定义图标，并且它可以在系统检测到介质或设备时自动启动应用程序以播放或显示内容。

本主题介绍如何为设备提供自定义图标。 Shell 和自动播放使用这些图标在 "自动播放"、"我的电脑" 和 "文件打开" 对话框中表示设备。 图标指示是否存在设备以及是否插入介质。 你可以提供以下图标：

-   *媒体插入图标*表示设备存在并且插入了介质。

-   "*无媒体插入" 图标*表示设备存在，但不插入 "中"。

除了为单独设备指定图标外，还可以指定用户定义的设备组或[设备安装程序类](device-setup-classes.md)中的所有设备的图标。 有关详细信息，请参阅[准备用于自动播放网站的硬件和软件](https://go.microsoft.com/fwlink/p/?linkid=12032)。

如果在[Windows 更新](https://docs.microsoft.com/windows-hardware/drivers)上发布了包含自定义图标的更新的[驱动程序包](driver-packages.md)，则系统会提示用户提供新下载。

在驱动程序包中包含图标文件有两个步骤：

1.  将图标文件添加到驱动程序包。

2.  在包的 INF 文件中，添加指定图标文件的条目，并将其复制到系统。

如果系统提供的驱动程序处理设备，则不必提供完整的[驱动程序包](driver-packages.md)。 只需提供一个 INF 文件和图标文件。 此 INF 文件必须包含所需的特定于图标的条目，并**包括**和**需要**引用系统提供的驱动程序 INF 文件中的设备安装部分的条目。

### <a name="to-create-icons"></a>创建图标

-   遵循创建[WINDOWS XP 图标](https://go.microsoft.com/fwlink/p/?linkid=6938)网站上提供的准则。 这些指南介绍了如何创建具有 Windows XP 图形元素外观和行为的图标。

### <a name="to-specify-the-icons-in-an-inf-file"></a>指定 INF 文件中的图标

-   在设备的[**Inf DDInstall 部分**](inf-ddinstall-hw-section.md)中包括一个[**inf AddReg 指令**](inf-addreg-directive.md)。 在 " **AddReg** " 部分中，指定 "**图标**" 和 " **NoMediaIcons** " 值项，如以下示例中所示：

    ```cpp
    [DDInstall.NT.HW]
    AddReg = IconInformation

    [IconInformation]
    HKR, , Icons, 0x10000, "media-inserted-icon-file"
    HKR, , NoMediaIcons, 0x10000, "no-media-inserted-icon-file"
    ```

    <a href="" id="icons"></a>**图标**  
    指定包含媒体插入图标的文件的名称。 *媒体插入图标文件*值是实际文件名的占位符。

    <a href="" id="nomediaicons"></a>**NoMediaIcons**  
    指定包含 "无媒体插入" 图标的文件的名称。 *无媒体插入图标文件*值是实际文件名的占位符。

### <a href="" id="to-direct-setup-to-copy-the-icon-files-to-the-system"></a>指示 Windows 将图标文件复制到系统

-   包括一个[**Inf SourceDisksFiles 部分**](inf-sourcedisksfiles-section.md)，其中列出了图标文件和一个将它们复制到系统的对应[**INF CopyFiles 指令**](inf-copyfiles-directive.md)。

Windows 会将 "**图标**" 和 " **NoMediaIcons** " 值项保存在设备的 "*硬件密钥*" 下的 "**设备参数**" 项下。 下面的示例为设备实例 ID 为 USB\\Vid_0000 & Pid_0000\\**059B003112010E93 的设备**指定注册表位置、值-输入类型**和值。**

**HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Enum\\** <em>USB\\Vid_0000 & Pid_0000\\059B003112010E93</em>\\**设备参数**

\[REG_MULTI_SZ\] 的**图标**=%*SystemRoo*t% *\\system32\\图标 .ico*

**NoMediaIcons** \[REG_MULTI_SZ\] =%*SystemRoot*% *\\system32\\noicon*

驱动程序或其他代码决不会直接访问或修改**设备参数**密钥。 应改为使用以下系统函数：

-   在用户模式下，使用[**SetupDiCreateDevRegKey**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedevregkeya)和[**SetupDiOpenDevRegKey**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendevregkey)。

-   在内核模式下，使用[**IoOpenDeviceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-ioopendeviceregistrykey)。

 

 





