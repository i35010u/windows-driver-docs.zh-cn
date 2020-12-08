---
title: 中间驱动程序通知对象
description: 中间驱动程序通知对象
keywords:
- 通知对象 WDK 网络，中间驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4da9338db78e1cab09a85698d1337be9d0d756d1
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96786141"
---
# <a name="intermediate-driver-notify-object"></a>中间驱动程序通知对象





*中间驱动程序通知对象* 是网络类安装程序的扩展。 网络类安装程序将加载并初始化通知对象，并向其发送事件通知 (如虚拟微端口删除通知) 与驱动程序相关的通知。 如果你需要概述通知对象的一般信息或有关通知对象的详细信息，请参阅 [为网络组件通知对象](notify-objects-for-network-components.md)。

若要在安装中包括通知对象，必须在中间驱动程序协议 INF 中引用它。 筛选中间驱动程序不需要通知对象。 如果希望为用户提供更灵活的配置选项，可以将通知对象包含在筛选器中间驱动程序中。

在 Windows Vista 上，你可以使用通知对象或自定义安装应用程序将微型端口 INF 文件复制到系统 INF 目录。 对于这两种情况，都使用 Microsoft Windows SDK 文档) 中所述的 **SetupCopyOEMInf** (来复制 INF。 对于 Windows Vista 和更高版本的操作系统版本，你应在协议 INF 中使用 [**INF CopyINF 指令**](../install/inf-copyinf-directive.md) 来复制微型端口 inf。 有关复制 INF 文件的详细信息，请参阅 [复制 inf](../install/copying-inf-files.md)。

MUX 中间驱动程序通知对象必须提供用于安装和删除虚拟微型端口的服务。 这可以自动完成，也可以通过提供用户界面来完成。 它必须在注册表中管理 virtual 微型端口的设备名称列表。 设备名称列表定义虚拟微型端口和物理设备之间的绑定。 例如，"多元 MUX 中间驱动程序示例" 通知对象维护一个虚拟微型端口列表，该列表绑定到 **UpperBindings** 注册表项中的每个物理设备。 MUX 示例驱动程序读取 **UpperBindings** 列表，并为每个条目初始化虚拟微型端口。

MUX 中间驱动程序应使用 **UpperRange** / **LowerRange** 项来控制外部绑定。 但是，如果需要，可以从通知对象控制外部绑定。 有关中间驱动程序中绑定的详细信息，请参阅 [中间驱动程序 UpperRange 和 LOWERRANGE INF 文件条目](intermediate-driver-upperrange-and-lowerrange-inf-file-entries.md)

通知对象可以选择提供一个用户界面，该用户界面允许用户更改或查看驱动程序的配置。 MUX 中间驱动程序示例包含通知对象的示例用户界面。

 

