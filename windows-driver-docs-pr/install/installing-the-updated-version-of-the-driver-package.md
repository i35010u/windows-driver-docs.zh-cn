---
title: 安装驱动程序包的已更新版本
description: 安装驱动程序包的已更新版本
ms.assetid: c2138956-a036-410d-b34e-b7b6efbcbace
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b88fdee7713ffa0602708b0215462654cc98b852
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63366539"
---
# <a name="installing-the-updated-version-of-the-driver-package"></a>安装驱动程序包的已更新版本


检查完[同样将 Windows 配置为排名驱动程序签名](configuring-windows-to-rank-driver-signatures-equally.md)，可以在目标系统上安装收件箱驱动程序的专用版本。 若要安装专用生成，请完成以下步骤：

1.  添加[驱动程序包](driver-packages.md)向驱动程序存储通过使用[PnPUtil](https://msdn.microsoft.com/library/windows/hardware/ff550419) Windows Vista 和更高版本的 Windows 中提供的实用工具。 例如：

    ```cpp
    pnputil.exe -a  sample.inf
    ```

2.  使用 DevCon Remove 命令删除的设备或设备类的情况下更新的驱动程序包安装。 通过全部或部分指定设备或设备类[硬件 ID](hardware-ids.md)，[兼容 ID](compatible-ids.md)，或设备的设备实例 ID。 例如：

    ```cpp
    devcon remove "PCI\VEN_8086&DEV_7110"
    ```

    重新启动系统后，重新安装设备时，会自动加载新的驱动程序。 若要让 DevCon 自动重新启动系统，添加条件的重新启动参数 (**/r**) 到 remove 命令。

    **请注意**   [DevCon](https://msdn.microsoft.com/library/windows/hardware/ff544707) WDK 中提供了工具。 有关其命令的详细信息，请参阅[DevCon 命令](https://msdn.microsoft.com/library/windows/hardware/ff544766)。

     

DevCon Remove 命令的替代方法是更新[驱动程序包](driver-packages.md)通过使用以下值之一：

-   若要执行"更新驱动程序"操作在设备上的设备管理器。

    在设备管理器窗口中，右键单击设备的名称或图标并选择**属性**。 在中**属性**窗口中，单击驱动程序选项卡，然后单击**更新驱动程序**按钮。

-   DevCon Update 命令。 有关此命令的详细信息，请参阅[ **DevCon 命令**](https://msdn.microsoft.com/library/windows/hardware/ff544766)。

 

 





