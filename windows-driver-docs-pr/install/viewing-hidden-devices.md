---
title: 查看隐藏的设备
description: 查看隐藏的设备
ms.assetid: 5dd02478-9937-4364-bd33-b64ac89c32eb
keywords:
- 虚幻设备 WDK
- 设备管理器 WDK，隐藏的设备
- 隐藏的设备 WDK
- DN_NO_SHOW_IN_DM
- 显示隐藏的设备
- 查看隐藏的设备
- 查看虚幻设备
- 显示虚幻设备
- 显示虚幻设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68c72c7891fee978af8fda9530d1396ea6134d5b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56547112"
---
# <a name="viewing-hidden-devices"></a>查看隐藏的设备

设备管理器列出计算机中安装的设备。 默认情况下，某些设备未显示在列表中。 这些*隐藏设备*包括：

* 设备具有设备节点 (devnode) 状态的位 DN_NO_SHOW_IN_DM 集。

    没有为计算机上每个设备 devnode，devnodes 被组织到层次结构的设备树。 配置设备时，即插即用管理器创建设备 devnode。

    Devnode 包含设备堆栈 （设备的驱动程序的设备对象） 和设备等设备是否已启动的驱动程序已注册的设备上的通知的信息。

* 设备安装程序类标记为属于**NoDisplayClass**注册表 （例如，打印机和非 PnP 驱动程序） 中

* 设备的已物理上从计算机中删除，但其注册表项不是已删除 （也称为虚幻设备）。

> [!NOTE]
> 从 Windows 8 和 Windows Server 2012 开始，即插即用播放管理器无法再创建为非 PnP （旧） 设备的设备表示形式。 因此，没有任何此类设备若要查看在设备管理器。

> [!NOTE]
> 用户应永远不需要查看虚幻的设备，因为虚幻设备不应具有他们的注意力，应该不会导致任何问题。 如果用户具有查看你的设备，如果不存在，则可能是您的驱动程序设计有问题。 但是，在测试期间，开发人员可能需要查看此类设备。

若要包括在设备管理器显示隐藏的设备，请单击**视图**，然后选择**显示隐藏的设备**。

Windows 8 之前，若要查看虚幻的设备，你必须设置环境变量 DEVMGR_SHOW_NONPRESENT_DEVICES 到**1**打开设备管理器之前，然后打开设备管理器，并在视图菜单上单击**显示隐藏设备**。

若要永久设置用户环境变量 DEVMGR_SHOW_NONPRESENT_DEVICES 到**1**，使用**高级**系统属性表选项卡。 设置此环境变量后，运行设备管理器并选择**显示隐藏的设备**。
