---
title: WIA DDI 接口
description: WIA DDI 接口
ms.assetid: 738a87e2-9c74-4215-85dc-ec793f10ce05
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d322ccde483705f32bac6354274f8be6fe762af8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367008"
---
# <a name="wia-ddi-interfaces"></a>WIA DDI 接口





WIA 的设备驱动程序接口 (DDI) 提供以下接口和函数的开发人员的 WIA 微型驱动程序：

-   [IWiaMiniDrv COM 接口](iwiaminidrv-com-interface.md)，其提供微型驱动程序的通信方法。 这些方法是 WIA 服务和微型驱动程序之间的所有通信的入口点。 这些方法启用 WIA 服务来控制设备。

-   [WIA 驱动程序服务库](wia-driver-services-library.md)(**wias * * * Xxx*函数)，后者为 WIA 微型驱动程序提供帮助器函数。 这些函数可用于执行许多常见任务，否则必须编写的自定义函数。

-   [WIA 的实用程序库](wia-utility-library.md)，其中提供了其他帮助器函数和三个类该 WIA 微型驱动程序可以使用。

-   [IWiaMiniDrvCallBack COM 接口](iwiaminidrvcallback-com-interface.md)，其中提供了 WIA 微型驱动程序，用于在回调数据传输过程中的回调方法。

-   [IWiaDrvItem COM 接口](iwiadrvitem-com-interface.md)，其中提供了用于微型驱动程序可以维护的设备的树方法**IWiaDrvItem**对象。

-   [用户界面扩展](user-interface-extensions.md)，它实现了供应商来提供功能，为不是通过默认 WIA 用户界面提供其设备。

-   [IWiaLog COM 接口](iwialog-com-interface.md)，这样的方法，并启用 WIA 微型驱动程序，以将消息记录到诊断日志文件的宏。

 

 




