---
title: WIA 微型驱动程序接口
description: WIA 微型驱动程序接口
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 247e53432d996afad3c0b99631c71bd43319e3ca
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826481"
---
# <a name="wia-minidriver-interfaces"></a>WIA 微型驱动程序接口





WIA 微型驱动程序是实现标准 **IUnknown** COM 接口 (的 com 对象，Microsoft Windows SDK 文档) 和另外两个特定于 WIA 的接口中对此进行了说明： [IStiUSD](istiusd-com-interface.md) 和 [IWiaMiniDrv](/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)。

### <a name="istiusd-interface"></a>IStiUSD 接口

在 *Stiusd* 中定义的 **IStiUSD** 接口执行以下操作：

-   WIA 服务首次加载时初始化驱动程序。

-   向 WIA 服务返回驱动程序的功能，并报告设备是否支持异步设备通知。

-   锁定和解锁设备以供独占使用。

### <a name="iwiaminidrv-interface"></a>IWiaMiniDrv 接口

在 *Wiamindr* 中定义的 **IWiaMiniDrv** 接口会公开大多数 WIA 微型驱动程序的功能。 此接口执行以下操作：

-   定义静止图像设备的默认设置和当前设置。

-   定义静止图像设备支持的命令和事件。

-   将数据从设备传输到 WIA 服务 (最终将其传递到调用应用程序) 。

有关这些接口的详细信息，请参阅 [开发 WIA 驱动程序：基本概念](developing-a-wia-driver--basic-concepts.md)。

 

