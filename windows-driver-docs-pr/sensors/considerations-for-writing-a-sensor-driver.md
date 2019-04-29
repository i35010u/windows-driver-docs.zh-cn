---
title: 有关编写传感器驱动程序的注意事项
description: 有关编写传感器驱动程序的注意事项
ms.assetid: fec3cfe8-43ad-481a-833a-6f38d04bfdef
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 29a7773e4c548578637842ed47aa8bb72bb078d0
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63357771"
---
# <a name="considerations-for-writing-a-sensor-driver"></a>有关编写传感器驱动程序的注意事项


编写传感器驱动程序之前，必须考虑以下关键问题。 此过程可帮助你做出各种设计和实现决策。

-   确定驱动程序支持多个传感器或单个传感器。 例如，你的硬件设备可能包含的传感器，组合，但可能会使用单个设备驱动程序。

-   确定需要在设备上交互的级别以及是否将发送回平台事件。 （大多数驱动程序和传感器解决方案，将支持事件。）传感器驱动程序事件的概述，请参阅[有关传感器驱动程序事件](about-sensor-driver-events.md)。

-   确定类别、 传感器类型和您的驱动程序的数据类型。 您可以决定使用一个平台定义的布局中，或自行定义。 该平台将传感器信息的组织的概述，请参阅[有关传感器常量](about-sensor-constants.md)

## <a name="related-topics"></a>相关主题
[传感器地理位置驱动程序示例](https://msdn.microsoft.com/library/windows/hardware/hh768273)  



