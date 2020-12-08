---
title: 网络组件的通知对象
description: 网络组件的通知对象
keywords:
- 通知对象 WDK 网络
- 网络通知对象 WDK
- 通知 WDK 网络
- 网络组件通知对象 WDK
- 显示属性页
- 属性页 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c77c861c033b852e4b6f28c45ee0919dbc259a4c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820567"
---
# <a name="notify-objects-for-network-components"></a>网络组件的通知对象





*通知对象* 代表特定网络组件来处理由网络配置子系统发送到对象的通知。 通知对象由动态链接库 (DLL) 提供。 通知对象用于显示网络组件的属性页，并提供组件对网络配置的编程控制。

**注意**  如果以下两个条件均为 true，则网络组件通常不需要 notify 对象：

 

-   可以通过信息 (INF) 文件中安装和删除网络组件

-   不需要对网络配置中的更改做出反应

以下各节描述了通知对象，并说明了如何开发它们：

[关于通知对象](about-notify-objects.md)

[创建通知对象](creating-a-notify-object.md)

有关支持通知对象的接口方法的参考信息，请参阅 [通知对象](/previous-versions/windows/hardware/network/ff559161(v=vs.85))。

 

