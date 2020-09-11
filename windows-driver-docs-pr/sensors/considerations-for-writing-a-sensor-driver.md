---
title: 编写传感器驱动程序的注意事项
description: 编写传感器驱动程序的注意事项
ms.assetid: fec3cfe8-43ad-481a-833a-6f38d04bfdef
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7defe8620b00396abd7ccdb584e553e33c3f639f
ms.sourcegitcommit: 937974aa9bbe0262a7ffe9631593fab48c4e7492
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/11/2020
ms.locfileid: "90009991"
---
# <a name="considerations-for-writing-a-sensor-driver"></a>编写传感器驱动程序的注意事项


编写传感器驱动程序之前，必须考虑以下关键问题。 此过程可帮助你做出各种设计和实现决策。

-   确定驱动程序是否支持多个传感器或单个传感器。 例如，硬件设备可能包含传感器的组合，但可能使用单个设备驱动程序。

-   确定设备上所需的交互级别，以及它是否会将事件发送回平台。  (大多数驱动程序和传感器解决方案都支持事件。 ) 有关传感器驱动程序事件的概述，请参阅 [关于传感器驱动程序事件](about-sensor-driver-events.md)。

-   确定驱动程序的类别、传感器类型和数据类型。 您可以决定使用某个平台定义的排列方式，也可以定义自己的排列方式。 有关平台如何组织传感器信息的概述，请参阅 [关于传感器常量](about-sensor-constants.md)

## <a name="related-topics"></a>相关主题
[传感器地理位置驱动程序示例](../gnss/sensors-geolocation-driver-sample.md)