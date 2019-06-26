---
title: 为 Shell 和自动播放提供供应商图标
description: 为 Shell 和自动播放提供供应商图标
ms.assetid: 2e3afbf6-57f6-4b83-b10a-c33d9b1c1731
keywords:
- 自动播放图标 WDK
- 自定义图标 WDK 设备安装
- 供应商图标 WDK
- WDK Shell 图标
- Shell 图标 WDK
- 媒体插入图标 WDK
- 无媒体插入图标 WDK
- WDK 自动播放图标
- 复制图标文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 495919e0be8910d3d6aedcddfd28abc65c29e002
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67386398"
---
# <a name="providing-vendor-icons-for-the-shell-and-autoplay"></a>为 Shell 和自动播放提供供应商图标





[自动播放](https://go.microsoft.com/fwlink/p/?linkid=12031)是 Shell 的扩展，支持的 Microsoft Windows XP 和更高版本的 Windows。 自动播放检测到不同类型的内容，例如音频或视频文件，请在可移动介质或可移动设备。 自动播放可以显示自定义图标的内容和设备，并且它可以自动启动应用程序来播放或当系统检测到的介质或设备时显示的内容。

本主题介绍如何为设备提供自定义图标。 Shell 和自动播放使用这些图标来表示自动播放、 我的电脑和文件打开的对话框中的设备。 图标指示设备是否存在以及是否插入介质。 你可以提供以下图标：

-   *媒体插入图标*指示设备已存在，并且插入介质。

-   *无媒体插入图标*指示该设备存在，但不是插入介质。

除了指定的单个设备的图标，你还可以指定的所有设备的图标的用户定义的设备组中或[设备安装程序类](device-setup-classes.md)。 有关详细信息，请参阅[准备硬件和软件以用于自动播放](https://go.microsoft.com/fwlink/p/?linkid=12032)网站。

如果更新[驱动程序包](driver-packages.md)包含一个自定义图标上发布[Windows Update](https://docs.microsoft.com/windows-hardware/drivers)，系统会提示用户是否有新的下载。

有两个步骤的驱动程序包中包括图标文件：

1.  将图标文件添加到驱动程序包。

2.  在包的 INF 文件中添加指定的图标文件并将其复制到系统的条目。

如果系统提供的驱动程序处理你的设备，不需要提供完整[驱动程序包](driver-packages.md)。 只需提供一个 INF 文件和图标文件。 此 INF 文件必须包含所需的特定于图标的条目，加上**Include**并**需要**指系统提供驱动程序的 INF 文件中的设备的安装部分的条目。

### <a name="to-create-icons"></a>若要创建图标

-   请遵循创建时提供的指导原则[Windows XP 图标](https://go.microsoft.com/fwlink/p/?linkid=6938)网站。 这些指导原则描述如何创建具有的外观和行为的 Windows XP 图形元素的图标。

### <a name="to-specify-the-icons-in-an-inf-file"></a>若要在 INF 文件中指定的图标

-   包括[ **INF AddReg 指令**](inf-addreg-directive.md)下[ **INF DDInstall.HW 部分**](inf-ddinstall-hw-section.md)设备。 在中**AddReg**部分中，指定**图标**并**NoMediaIcons**值项，如下面的示例中所示：

    ```cpp
    [DDInstall.NT.HW]
    AddReg = IconInformation

    [IconInformation]
    HKR, , Icons, 0x10000, "media-inserted-icon-file"
    HKR, , NoMediaIcons, 0x10000, "no-media-inserted-icon-file"
    ```

    <a href="" id="icons"></a>**图标**  
    指定包含的媒体插入图标的文件的名称。 *媒体插入文件形式的图标*值是一个占位符的实际文件名称。

    <a href="" id="nomediaicons"></a>**NoMediaIcons**  
    指定包含无媒体插入图标的文件的名称。 *否-媒体-插入的图标的文件*值是一个占位符的实际文件名称。

### <a href="" id="to-direct-setup-to-copy-the-icon-files-to-the-system"></a>若要指示 Windows 图标文件复制到系统

-   包括[ **INF SourceDisksFiles 部分**](inf-sourcedisksfiles-section.md) ，它列出的图标文件和相应[ **INF CopyFiles 指令**](inf-copyfiles-directive.md) ，用于复制它们对系统。

Windows 将保存**图标**并**NoMediaIcons**值下的条目**设备参数**下设备的密钥*硬件密钥*。 下面的示例指定的注册表位置、 值项类型和值**图标**并**NoMediaIcons**值为其设备实例 ID 是 USB 设备的条目\\Vid_0000 & Pid_0000\\059B003112010E93。

**HKEY_LOCAL_MACHINE\\SYSTEM\\CurrentControlSet\\Enum\\** <em>USB\\Vid_0000&Pid_0000\\059B003112010E93</em>\\**Device Parameters**

**Icons** \[REG_MULTI_SZ\] = %*SystemRoo*t% *\\system32\\icon.ico*

**NoMediaIcons** \[REG_MULTI_SZ\] = %*SystemRoot*% *\\system32\\noicon.ico*

驱动程序或其他代码应永远不会访问或修改**设备参数**直接密钥。 相反，应使用以下系统函数：

-   从用户模式下，使用[ **SetupDiCreateDevRegKey** ](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdicreatedevregkeya)并[ **SetupDiOpenDevRegKey**](https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupdiopendevregkey)。

-   从内核模式下，使用[ **IoOpenDeviceRegistryKey**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-ioopendeviceregistrykey)。

 

 





