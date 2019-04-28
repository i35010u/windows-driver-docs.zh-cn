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
ms.openlocfilehash: 1de7f990d6c7e3a445931d8f8848d9a3f25b2df9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63331839"
---
# <a name="notify-objects-for-network-components"></a>网络组件的通知对象





一个*通知对象*处理通过代表特定的网络组件的对象的网络配置子系统发送通知。 通知对象被提供动态链接库 (DLL)。 通知对象用于显示网络组件的属性页并使该组件以编程方式控制对网络配置。

**请注意**  网络组件一般不需要进行通知对象如果以下条件都成立：

 

-   可以安装和删除其信息 (INF) 文件通过网络组件

-   对网络配置中的更改做出反应并不要求

以下各节介绍通知对象，并介绍了如何开发它们：

[有关通知的对象](about-notify-objects.md)

[创建通知对象](creating-a-notify-object.md)

有关参考信息为接口方法支持通知对象，请参阅[通知对象](https://msdn.microsoft.com/library/windows/hardware/ff559161)。

 

 





