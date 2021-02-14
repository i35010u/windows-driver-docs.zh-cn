---
title: 使用设备管理器卸载设备和驱动程序包
description: 使用设备管理器卸载设备和驱动程序包
ms.date: 10/07/2020
ms.localizationpriority: medium
ms.custom: contperf-fy21q2
ms.openlocfilehash: 26d940c5af32b837e9ce8995ab8703ad02dee23a
ms.sourcegitcommit: 76698e25b77af71155e689200c6e0cf817bfd0d7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2021
ms.locfileid: "100262261"
---
# <a name="using-device-manager-to-uninstall-devices-and-driver-packages"></a>使用设备管理器卸载设备和驱动程序包

本页介绍如何在 Windows 10 上卸载设备或驱动程序包。  在卸载设备之前，建议从系统中拔出设备。  如果设备在被拔出之前已卸载，则操作系统可能会重新发现设备，并在卸载并拔出设备之间的时间内为其指定新设置。

首先，打开 "设置" (可以使用 `Windows+I` 键盘快捷方式) 并键入 "删除" 来执行此操作。 选择 " **添加或删除程序**"。 如果要删除的设备或驱动程序包出现在程序列表中，请选择 "卸载"。

如果设备或驱动程序包未出现在列表中，则可以通过 Device Manager 卸载设备。  如果该设备是使用驱动程序包的唯一设备，则也可以通过 Device Manager 删除驱动程序包。  若要启动 Device Manager，请单击 "开始" 按钮，键入 Device Manager，然后按 Enter。

然后执行以下步骤：

1. 单击 "查看" 菜单并打开 "显示隐藏的设备"
2. 展开表示要卸载的设备类型的节点，右键单击要卸载的设备的设备条目，并选择 " **卸载**"。
2. 在 " **确认设备删除** " 对话框中，如果除了卸载设备之外还希望删除驱动程序包，请选择 " **删除此设备的驱动程序软件** " 选项。 准备好完成操作后，请选择 **"确定"**。

在某些设备上，如果在卸载设备时设备仍接通电源，则设备可能会继续运行，直到重新启动系统。

有关卸载驱动程序包和驱动程序包的详细信息，请参阅 [如何卸载设备和驱动程序包](how-devices-and-driver-packages-are-uninstalled.md)。
