---
title: WIA 驱动程序事件支持
description: WIA 驱动程序事件支持
ms.assetid: 544c756b-4222-4d59-8393-924d3691e0f8
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b09ce9ffcf2543dd93d447647a11e6bf19bc182e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575800"
---
# <a name="wia-driver-event-support"></a>WIA 驱动程序事件支持





有两种类型的可支持 WIA 微型驱动程序的事件机制：

<a href="" id="interrupt-events"></a>中断事件  
每次操作发生在设备上时，设备会将未经请求的异步通知发送到微型驱动程序。

<a href="" id="polling-events"></a>轮询事件  
WIA 服务会定期询问微型驱动程序来查询该设备以确定是否发生了任何新的事件。 默认情况下，WIA 服务每隔一秒轮询该驱动程序。 此值是可配置设备的 INF 文件中 (请参阅[WIA 设备 INF 文件](inf-files-for-wia-devices.md)有关详细信息)。

可以在 WIA 微型驱动程序中使用这些事件机制之一。 中断事件机制被建议，因为更高的可靠性和性能。

有三种支持的事件机制。

1.  在 Windows Me，STI 事件启动已注册的 STI 事件的应用程序。 此应用程序打开设备的 TWAIN 数据源。

2.  Windows Me 中，Windows XP 和更高版本，WIA 事件启动已注册的 WIA 事件的应用程序。 此应用程序使用 WIA 服务来访问设备。

3.  在 Windows XP 及更高版本，WIA 服务将 WIA 事件转换成 STI STI 事件已注册的应用程序的事件。 此应用程序使用了 TWAIN WIA TWAIN 通过访问设备的兼容性层。

本部分包含以下主题：

[添加中断事件支持](adding-interrupt-event-support.md)

[添加轮询事件支持](adding-polling-event-support.md)

[提供事件通知](providing-event-notification.md)

 

 




