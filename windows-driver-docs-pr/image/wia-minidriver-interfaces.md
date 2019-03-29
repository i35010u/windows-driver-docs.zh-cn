---
title: WIA 微型驱动程序接口
description: WIA 微型驱动程序接口
ms.assetid: 6d069584-f9e1-4312-b8f2-1ef3d518faeb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2442972a981387a344df5d1b0d11533d4748b75b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568449"
---
# <a name="wia-minidriver-interfaces"></a>WIA 微型驱动程序接口





WIA 微型驱动程序是实现标准的 COM 对象**IUnknown** COM 接口 （这 Microsoft Windows SDK 文档中所述） 和两个其他特定于 WIA 的接口：[IStiUSD](istiusd-com-interface.md)并[IWiaMiniDrv](https://msdn.microsoft.com/library/windows/hardware/ff545027)。

### <a name="istiusd-interface"></a>IStiUSD 接口

**IStiUSD**中定义的接口*Stiusd.h*，执行以下操作：

-   WIA 服务首次加载时初始化该驱动程序。

-   返回到 WIA 服务，报告此设备是否支持异步设备通知驱动程序的功能。

-   锁定和解锁该设备进行独占使用。

### <a name="iwiaminidrv-interface"></a>IWiaMiniDrv 接口

**IWiaMiniDrv**中定义的接口*Wiamindr.h*，公开大多数 WIA 微型驱动程序的功能。 此接口将执行以下操作：

-   定义静态图像设备的默认值和当前设置。

-   定义静态图像设备的受支持的命令和事件。

-   将数据从设备传输到 WIA 服务 （它最终将其传递到调用应用程序）。

有关这些接口的详细信息，请参阅[开发 WIA 驱动程序：基本概念](developing-a-wia-driver--basic-concepts.md)。

 

 




