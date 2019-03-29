---
title: 规划器微型类驱动程序简介
description: 规划器微型类驱动程序简介
ms.assetid: ce0f78a3-69ae-4ca7-b2e1-f4892e35a230
keywords:
- 更换器驱动程序 WDK 存储，miniclass 驱动程序
- 存储更换器驱动程序 WDK，miniclass 驱动程序
- miniclass 驱动程序 WDK 换带机
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a5dea73e27243821da5ee8c8de3501b91b33052b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56562857"
---
# <a name="introduction-to-changer-miniclass-drivers"></a>规划器微型类驱动程序简介


## <span id="ddk_introduction_to_changer_miniclass_drivers_kg"></span><span id="DDK_INTRODUCTION_TO_CHANGER_MINICLASS_DRIVERS_KG"></span>


若要支持新的转换器，驱动程序编写器实现换带机 miniclass 驱动程序链接到的系统提供的转换器类驱动程序。 必须编写新的转换器 miniclass 驱动程序只是为了支持系统不会不已提供相关的驱动程序换带机。

在开始之前实现新的 miniclass 驱动程序，您应确保：

-   设备是 true 转换器和集不串行访问纸器。 换带机允许在随机顺序，而不是固定的序列，如集纸器中所示其驱动器中装入媒体。

-   设备的驱动器不是写入-一旦光学介质驱动器，如蠕虫病毒爆发、 CD R 或 DVD-R。

-   设备的驱动器的所有相同类型，因为使用的类型，如 CD-ROM 和 CD。

Microsoft 操作系统不支持写入-一次光学介质驱动器或更换器使用多个驱动器的类型。

 

 




