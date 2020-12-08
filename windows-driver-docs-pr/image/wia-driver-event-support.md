---
title: WIA 驱动程序事件支持
description: WIA 驱动程序事件支持
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 892e8bb07dc8c0688190bb60520665fbed8ea43d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830025"
---
# <a name="wia-driver-event-support"></a>WIA 驱动程序事件支持





WIA 微型驱动程序可以支持两种类型的事件机制：

<a href="" id="interrupt-events"></a>中断事件  
当设备上发生操作时，设备将向微型驱动程序发送未经请求的异步通知。

<a href="" id="polling-events"></a>轮询事件  
WIA 服务会定期请求微型驱动程序查询设备，以确定是否有任何新事件发生。 默认情况下，WIA 服务每秒轮询驱动程序。 此值可在设备的 INF 文件中配置 (参阅用于 [WIA 设备的 Inf 文件](inf-files-for-wia-devices.md) 了解详细信息) 。

WIA 微型驱动程序中只能使用其中一种事件机制。 由于可靠性和性能提高，因此建议使用中断事件机制。

有三种受支持的事件机制。

1.  在 Windows Me 中，STI 事件会启动已注册 STI 事件的应用程序。 此应用程序打开设备的 TWAIN 数据源。

2.  在 Windows Me、Windows XP 和更高版本中，WIA 事件会启动已为 WIA 事件注册的应用程序。 此应用程序使用 WIA 服务来访问设备。

3.  在 Windows XP 和更高版本中，WIA 服务会将 WIA 事件转换为已注册为 STI 事件的应用程序的 STI 事件。 此应用程序使用 TWAIN 到 WIA 兼容性层通过 TWAIN 访问设备。

本节包含下列主题：

[添加中断事件支持](adding-interrupt-event-support.md)

[添加轮询事件支持](adding-polling-event-support.md)

[提供事件通知](providing-event-notification.md)

 

 




