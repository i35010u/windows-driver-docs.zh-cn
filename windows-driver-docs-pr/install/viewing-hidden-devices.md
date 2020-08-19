---
title: 查看隐藏的设备
description: 查看隐藏的设备
ms.assetid: 5dd02478-9937-4364-bd33-b64ac89c32eb
keywords:
- nonpresent 设备 WDK
- 设备管理器 WDK，隐藏设备
- 隐藏设备 WDK
- DN_NO_SHOW_IN_DM
- 显示隐藏的设备
- 查看隐藏的设备
- 查看 nonpresent 设备
- 显示 nonpresent 设备
- 显示 nonpresent 设备
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fed3bc410bc304b79f3a1604c67a863e48570a85
ms.sourcegitcommit: f5222e608f2853003175244505d5daa3465ac6b3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/19/2020
ms.locfileid: "88615079"
---
# <a name="viewing-hidden-devices"></a>查看隐藏的设备

设备管理器列出计算机上安装的设备。 默认情况下，某些设备不会显示在列表中。 这些 *隐藏设备* 包括：

* 设备节点 (devnode) 状态位 DN_NO_SHOW_IN_DM 设置的设备。

    计算机上的每个设备都有一个 devnode，devnodes 被组织成一个分层设备树。 配置设备时，PnP 管理器会为设备创建一个 devnode。

    Devnode 包含设备 (设备驱动程序的设备对象) 和设备信息，例如设备是否已启动以及哪些驱动程序已在设备上注册了通知。

* 属于注册表 (中标记为 **NoDisplayClass** 的安装程序类的设备，例如，打印机和非 PnP 驱动程序) 

* 物理上从计算机中删除但未删除其注册表项的设备 (也称为 nonpresent 设备) 。

> [!NOTE]
> 从 Windows 8 和 Windows Server 2012 开始，即插即用管理器不再为非 PnP (旧) 设备创建设备表示。 因此，设备管理器中没有要查看的设备。

> [!NOTE]
> 用户永远不需要查看 nonpresent 设备，因为 nonpresent 设备不应注意并不会导致任何问题。 如果用户在设备不存在时必须查看设备，可能是驱动程序设计有问题。 但是，在测试期间，开发人员可能需要查看此类设备。

若要在设备管理器显示中包括隐藏设备，请选择 " **查看** "，然后选择 " **显示隐藏的设备**"。

在 Windows 8 之前，若要查看 nonpresent 设备，必须在打开设备管理器之前将环境变量 DEVMGR_SHOW_NONPRESENT_DEVICES 设置为 **1** ，然后打开设备管理器，然后在 "视图" 菜单上，选择 " **显示隐藏的设备**"。

若要将用户环境变量 DEVMGR_SHOW_NONPRESENT_DEVICES 设置为 **1**，请使用系统属性表的 " **高级** " 选项卡。 设置此环境变量后，请运行设备管理器，然后选择 " **显示隐藏的设备**"。
