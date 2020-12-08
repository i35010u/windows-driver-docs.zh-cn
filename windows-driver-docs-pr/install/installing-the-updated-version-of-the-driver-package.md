---
title: 安装驱动程序包的已更新版本
description: 安装驱动程序包的已更新版本
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 81d56d89968bc4bcb2ce7c1e3def1a890426d2df
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791729"
---
# <a name="installing-the-updated-version-of-the-driver-package"></a>安装驱动程序包的已更新版本


[将 Windows 配置为按比例排列驱动程序签名](configuring-windows-to-rank-driver-signatures-equally.md)后，可以在目标系统上安装收件箱驱动程序的专用生成。 若要安装专用生成，请完成以下步骤：

1.  使用 Windows Vista 和更高版本的 Windows 中提供的[PnPUtil](../devtest/pnputil.md)实用程序，将[驱动程序包](driver-packages.md)添加到驱动程序存储区。 例如：

    ```cpp
    pnputil.exe -a  sample.inf
    ```

2.  使用 DevCon Remove 命令删除已更新的驱动程序包安装的设备或设备类。 设备或设备类是通过设备的全部或部分 [硬件 ID](hardware-ids.md)、 [兼容 ID](compatible-ids.md)或设备实例 ID 指定的。 例如：

    ```cpp
    devcon remove "PCI\VEN_8086&DEV_7110"
    ```

    重新启动系统后重新安装设备后，会自动加载新的驱动程序。 若要让 DevCon 自动重新启动系统，请将 (**/r**) 的条件重新启动参数添加到 "删除" 命令。

    **注意**  在 WDK 中提供了 [DevCon](../devtest/devcon.md) 工具。 有关其命令的详细信息，请参阅 [DevCon 命令](../devtest/devcon-general-commands.md)。

     

DevCon Remove 命令的替代方法是使用以下命令之一更新 [驱动程序包](driver-packages.md) ：

-   设备管理器在设备上执行 "更新驱动程序" 操作。

    在设备管理器窗口中，右键单击设备的名称或图标，然后选择 " **属性**"。 在 " **属性** " 窗口中，单击 "驱动程序" 选项卡，然后单击 " **更新驱动程序** " 按钮。

-   DevCon Update 命令。 有关此命令的详细信息，请参阅 [**DevCon 命令**](../devtest/devcon-general-commands.md)。

 

