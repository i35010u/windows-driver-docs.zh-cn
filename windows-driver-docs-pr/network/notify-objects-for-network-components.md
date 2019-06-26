---
title: 网络组件的通知对象
description: 网络组件的通知对象
ms.assetid: 5b5c5da2-7163-44cf-8e8a-c736278f2535
keywords:
- 通知对象 WDK 网络
- 网络通知对象 WDK
- 通知 WDK 网络
- 通知对象 WDK，网络组件
- 显示属性页
- 属性页 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 66be6a9120c3ffbc619b84c362691376759b6cdc
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354536"
---
# <a name="notify-objects-for-network-components"></a>网络组件的通知对象





一个*通知对象*处理通过代表特定的网络组件的对象的网络配置子系统发送通知。 通知对象被提供动态链接库 (DLL)。 通知对象用于显示网络组件的属性页并使该组件以编程方式控制对网络配置。

**请注意**  网络组件一般不需要进行通知对象如果以下条件都成立：

 

-   可以安装和删除其信息 (INF) 文件通过网络组件

-   对网络配置中的更改做出反应并不要求

以下各节介绍通知对象，并介绍了如何开发它们：

[有关通知的对象](about-notify-objects.md)

[创建通知对象](creating-a-notify-object.md)

有关参考信息为接口方法支持通知对象，请参阅[通知对象](https://docs.microsoft.com/previous-versions/windows/hardware/network/ff559161(v=vs.85))。

 

 





