---
title: WIA 驱动程序组件
description: WIA 驱动程序组件
ms.assetid: 2c854945-2eda-4f4c-9cf6-5525e6e237ed
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0259378d1374fce9e2763c7975095b02eaccc5b0
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185023"
---
# <a name="wia-driver-components"></a>WIA 驱动程序组件





WIA 微型驱动程序可以视为两个逻辑层：

-   WIA 服务接口层

-   设备通信层

下图说明了 WIA 微型驱动程序及其组件的逻辑细目。

![阐释 wia 微型驱动程序及其组件的关系图](images/art-minidrv.png)

### <a name="wia-minidriver-interfaces"></a>WIA 微型驱动程序接口

WIA 微型驱动程序是实现 **IUnknown** com 接口和两个特定于 WIA 的 com 接口的 com 对象： [IStiUSD](istiusd-com-interface.md) 和 [IWiaMiniDrv](/windows-hardware/drivers/ddi/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)。 WIA 微型驱动程序接口层实现这些接口，是 WIA 微型驱动程序的入口点。 应用程序不直接调用 WIA 微型驱动程序接口;只有 WIA 服务调用这些接口。

### <a name="device-communication"></a>设备通信

设备通信层负责通过内核模式总线驱动程序与静止图像设备的低级交互。 与设备的所有交互都通过此层发送。 此层负责将数据打包为物理设备可以理解的格式，并将数据从设备收到的 unpackaging 数据转换为驱动程序可以理解的格式。

本部分提供有关 WIA 微型驱动程序及其组件在以下方面的其他信息：

[WIA 微型驱动程序接口](wia-minidriver-interfaces.md)

[通过总线驱动程序进行的设备通信](device-communication-through-the-bus-driver.md)

[WIA 组件](wia-components.md)

 

