---
title: WIA 微型驱动程序接口
description: WIA 微型驱动程序接口
ms.assetid: 6d069584-f9e1-4312-b8f2-1ef3d518faeb
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5ee0ffb88e52755355ab565fbbcef502342e0a44
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355186"
---
# <a name="wia-minidriver-interfaces"></a>WIA 微型驱动程序接口





WIA 微型驱动程序是实现标准的 COM 对象**IUnknown** COM 接口 （这 Microsoft Windows SDK 文档中所述） 和两个其他特定于 WIA 的接口：[IStiUSD](istiusd-com-interface.md)并[IWiaMiniDrv](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)。

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

 

 




