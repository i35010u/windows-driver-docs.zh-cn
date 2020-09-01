---
title: 关于通知对象
description: 关于通知对象
ms.assetid: 87e4bcb6-dbdc-487d-9e21-0738165bf834
keywords:
- 通知对象 WDK 网络，关于通知对象
- 网络通知对象 WDK，关于通知对象
- 通知 WDK 网络，关于通知对象
- 网络配置子系统 WDK
- 子系统 WDK 网络配置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2d380e837e993f46e01c9a913d3b0f6b965fbee2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89214069"
---
# <a name="about-notify-objects"></a>关于通知对象





通知对象处理网络配置子系统代表特定网络组件发送到对象的通知。 此网络组件拥有 notify 对象。 可以拥有通知对象的网络组件包括：

-   传输，如协议驱动程序

-   诸如中间驱动程序之类的服务

-   客户端，如 Microsoft 网络客户端

**注意**   网卡不支持且无法拥有通知对象。 加入配置网络或安装和卸载的物理或虚拟网卡必须使用 INF 文件或设备共同安装程序机制。
有关详细信息，请参阅 [编写共同安装程序](../install/writing-a-co-installer.md)。

 

Notify 对象执行以下操作：

-   向网络配置子系统公开接口方法，使网络配置子系统可以通知通知对象关于通知对象请求通知的事件。

-   调用网络配置子系统的公共接口的方法，以执行包括但不限于安装和删除网络设备的操作。 有关详细信息，请参阅 [网络配置接口](/previous-versions/windows/hardware/network/ff559080(v=vs.85))。

若要请求和接收通知并相互通信，通知对象和网络配置子系统 (COM) 接口实现组件对象模型。

通知对象是驻留在动态链接库中 (Dll) 的 COM 对象。 这些 Dll 是 COM *组件服务器*。 每种类型的网络组件都与安装特定类型的网络组件并注册这些网络组件所拥有的 COM*类对象*的*类安装程序*相关联。 网络组件的主要安装阶段完成后，将注册对象。 若要注册 COM 类对象，类安装程序将调用该对象的 DLL 入口点函数。

只要操作系统安装、升级或删除网络功能，或者在应用程序配置网络时，操作系统或这些应用程序都必须启动网络配置子系统。 网络配置子系统启动后，将创建一个通知对象的实例，并且通知对象将执行特定的操作。

以下主题描述通知对象接收的通知类型和通知对象执行的操作：

[通知对象示意图](notify-object-diagram.md)

[处理通知](processing-notifications.md)

[安装网络组件](installing-network-components.md)

[删除网络组件](removing-network-components.md)

[升级网络组件](upgrading-network-components.md)

[显示和更改属性](displaying-and-changing-properties.md)

[配置网络](configuring-the-network.md)

 

