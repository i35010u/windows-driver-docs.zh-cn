---
title: WIA 微型驱动程序接口
description: WIA 微型驱动程序接口
ms.assetid: 6d069584-f9e1-4312-b8f2-1ef3d518faeb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fb3139e10bab9a6c3cabeb1c911e47aa51d26877
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840676"
---
# <a name="wia-minidriver-interfaces"></a>WIA 微型驱动程序接口





WIA 微型驱动程序是一个 COM 对象，它实现了标准**IUnknown** COM 接口（在 Microsoft Windows SDK 文档中进行了介绍）和两个附加的 WIA 特定接口： [IStiUSD](istiusd-com-interface.md)和[IWiaMiniDrv](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)。

### <a name="istiusd-interface"></a>IStiUSD 接口

在*Stiusd*中定义的**IStiUSD**接口执行以下操作：

-   WIA 服务首次加载时初始化驱动程序。

-   向 WIA 服务返回驱动程序的功能，并报告设备是否支持异步设备通知。

-   锁定和解锁设备以供独占使用。

### <a name="iwiaminidrv-interface"></a>IWiaMiniDrv 接口

在*Wiamindr*中定义的**IWiaMiniDrv**接口会公开大多数 WIA 微型驱动程序的功能。 此接口执行以下操作：

-   定义静止图像设备的默认设置和当前设置。

-   定义静止图像设备支持的命令和事件。

-   将数据从设备传输到 WIA 服务（最终将其传递到调用应用程序）。

有关这些接口的详细信息，请参阅[开发 WIA 驱动程序：基本概念](developing-a-wia-driver--basic-concepts.md)。

 

 




