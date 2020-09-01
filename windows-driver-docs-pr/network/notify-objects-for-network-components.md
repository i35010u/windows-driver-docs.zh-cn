---
title: 网络组件的通知对象
description: 网络组件的通知对象
ms.assetid: 5b5c5da2-7163-44cf-8e8a-c736278f2535
keywords:
- 通知对象 WDK 网络
- 网络通知对象 WDK
- 通知 WDK 网络
- 网络组件通知对象 WDK
- 显示属性页
- 属性页 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f23d0e633e3f27467b5b2eeb53857b4d1b00af0a
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216150"
---
# <a name="notify-objects-for-network-components"></a>网络组件的通知对象





*通知对象*代表特定网络组件来处理由网络配置子系统发送到对象的通知。 通知对象由动态链接库 (DLL) 提供。 通知对象用于显示网络组件的属性页，并提供组件对网络配置的编程控制。

**注意**   如果以下两个条件均为 true，则网络组件通常不需要 notify 对象：

 

-   可以通过信息 (INF) 文件中安装和删除网络组件

-   不需要对网络配置中的更改做出反应

以下各节描述了通知对象，并说明了如何开发它们：

[关于通知对象](about-notify-objects.md)

[创建通知对象](creating-a-notify-object.md)

有关支持通知对象的接口方法的参考信息，请参阅 [通知对象](/previous-versions/windows/hardware/network/ff559161(v=vs.85))。

 

