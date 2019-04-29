---
title: 关于通知对象
description: 关于通知对象
ms.assetid: 87e4bcb6-dbdc-487d-9e21-0738165bf834
keywords:
- 通知对象 WDK 网络，大约通知对象
- 网络通知对象 WDK，大约通知对象
- 通知 WDK 大约网络、 通知对象
- 网络配置子系统 WDK
- 子系统 WDK 网络配置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 651e61b0c18fe7cee505042249248d41357d36d3
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367910"
---
# <a name="about-notify-objects"></a>关于通知对象





通知对象处理网络配置子系统将发送到特定的网络组件代表对象的通知。 此网络组件拥有通知对象。 可以拥有通知对象的网络组件包括：

-   传输如协议驱动程序

-   服务，如中间驱动程序

-   例如，Microsoft 网络客户端的客户端

**请注意**  网络卡不支持，并且不能拥有通知对象。 参与是配置网络或安装和卸载的物理或虚拟网络卡必须使用 INF 文件或设备共同安装程序机制。
有关详细信息，请参阅[编写共同安装程序](https://msdn.microsoft.com/library/windows/hardware/ff554011)。

 

通知对象执行以下操作：

-   公开接口到网络配置子系统的方法，以便网络配置子系统可以通知的事件通知对象在其请求发送通知的匹配项的通知对象。

-   调用方法的网络配置子系统的公共接口来执行操作，其中包括但不限于安装和删除网络设备。 有关详细信息，请参阅[网络配置接口](https://msdn.microsoft.com/library/windows/hardware/ff559080)。

请求和接收通知以及与彼此通信，通知对象和网络配置子系统实现组件对象模型 (COM) 接口。

通知对象是驻留在动态链接库 (Dll) 内的 COM 对象。 这些 Dll 是 COM*组件服务器*。 每种类型的网络组件与*类安装程序*后者安装特定类型的网络组件并注册 COM*类对象*归这些网络组件。 网络组件的安装阶段完成后，注册对象。 若要注册的 COM 类对象，类安装程序将调用对象的 DLL 入口点函数。

每当在操作系统安装、 升级或删除网络功能或操作系统或这些应用程序时应用程序配置的网络，必须启动网络配置子系统。 网络配置子系统启动后，它创建的通知对象实例，并通知对象执行特定操作。

以下主题介绍的通知的通知对象接收和执行的操作的通知对象的类型：

[通知对象关系图](notify-object-diagram.md)

[处理通知](processing-notifications.md)

[安装网络组件](installing-network-components.md)

[删除网络组件](removing-network-components.md)

[升级网络组件](upgrading-network-components.md)

[显示和更改属性](displaying-and-changing-properties.md)

[配置网络](configuring-the-network.md)

 

 





