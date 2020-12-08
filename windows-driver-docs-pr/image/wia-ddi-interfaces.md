---
title: WIA DDI 接口
description: WIA DDI 接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 364793e6800270f5558a4f4db5f3f7ef2a78e2a9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824547"
---
# <a name="wia-ddi-interfaces"></a>WIA DDI 接口





WIA 设备驱动程序接口 (DDI) 为 WIA 微型驱动程序的开发人员提供以下接口和功能：

-   [IWIAMINIDRV COM 接口](iwiaminidrv-com-interface.md)，提供微型驱动程序通信方法。 这些方法是 WIA 服务与微型驱动程序之间的所有通信的入口点。 这些方法允许 WIA 服务控制设备。

-   [Wia 驱动程序服务库](wia-driver-services-library.md) (**wias**_XXX_ 函数) ，为 WIA 微型驱动程序提供 helper 函数。 您可以使用这些函数来执行许多常见任务，否则您必须编写自定义函数。

-   [Wia 实用工具库](wia-utility-library.md)，提供其他 helper 函数和 WIA 微型驱动程序可以使用的三个类。

-   [IWIAMINIDRVCALLBACK COM 接口](iwiaminidrvcallback-com-interface.md)，该接口为 WIA 微型驱动程序提供回调方法，以便在回调数据传输过程中使用。

-   [IWIADRVITEM COM 接口](iwiadrvitem-com-interface.md)，为微型驱动程序提供用于维护设备的 **IWiaDrvItem** 对象树的方法。

-   [用户界面扩展](user-interface-extensions.md)，使供应商能够为其设备提供未通过默认 WIA 用户界面提供的功能。

-   [IWIALOG COM 接口](iwialog-com-interface.md)，它提供允许 WIA 微型驱动程序将消息记录到诊断日志文件的方法和宏。

 

 




