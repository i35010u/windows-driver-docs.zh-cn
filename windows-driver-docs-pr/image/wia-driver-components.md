---
title: WIA 驱动程序组件
description: WIA 驱动程序组件
ms.assetid: 2c854945-2eda-4f4c-9cf6-5525e6e237ed
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab7460db9c4b59e609d807bdb21600cf53134ea0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383780"
---
# <a name="wia-driver-components"></a>WIA 驱动程序组件





WIA 微型驱动程序可被视为两个逻辑层：

-   WIA 服务接口层

-   设备的通信层

下图说明了 WIA 微型驱动程序及其组件的逻辑的细分。

![说明 wia 微型驱动程序和其组件的关系图](images/art-minidrv.png)

### <a name="wia-minidriver-interfaces"></a>WIA 微型驱动程序接口

WIA 微型驱动程序为 COM 对象实现**IUnknown** COM 接口和两个特定于 WIA 的 COM 接口：[IStiUSD](istiusd-com-interface.md)并[IWiaMiniDrv](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nn-wiamindr_lh-iwiaminidrv)。 WIA 微型驱动程序接口层将实现这些接口，将 WIA 微型驱动程序的入口点。 应用程序不直接; 调用 WIA 微型驱动程序接口仅 WIA 服务调用这些接口。

### <a name="device-communication"></a>设备的通信

设备的通信层负责与内核模式总线驱动程序通过在静止图像设备的低级别交互。 通过此层发送的与设备的所有交互。 这一层负责打包数据为物理设备可以理解的格式发送到设备并 unpackaging 数据从设备接收到该驱动程序理解的格式。

本部分提供有关 WIA 微型驱动程序及其组件的以下区域中的其他信息：

[WIA 微型驱动程序接口](wia-minidriver-interfaces.md)

[通过总线驱动程序设备通信](device-communication-through-the-bus-driver.md)

[WIA 组件](wia-components.md)

 

 




