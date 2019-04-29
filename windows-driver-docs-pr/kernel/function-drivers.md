---
title: 函数驱动程序
description: 函数驱动程序
ms.assetid: a6ac329b-ffb0-4bd3-9d54-195fa025d532
keywords:
- 函数的 WDK WDM 驱动程序
- raw 模式 WDK WDM
- WDM 函数驱动程序 WDK
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 17397b0c68258dc7db5e6dd86a5c285c7af9a4f9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63359945"
---
# <a name="function-drivers"></a>函数驱动程序





一个*功能驱动程序*是设备的主要驱动程序 （请参阅可能的驱动程序层）。 PnP 管理器将加载最多一个函数设备驱动程序。 功能驱动程序可以服务一个或多个设备。

功能驱动程序提供用于其设备的操作的接口。 功能驱动程序通常处理读取和写入设备并管理设备的电源策略。

可以作为驱动程序/微型驱动程序对，如端口/微型端口驱动程序对或类/miniclass 驱动程序对实现设备功能驱动程序。 在此类驱动程序对，微型驱动程序链接到第二个驱动程序，这是一个 DLL。

如果设备驱动在 raw 模式，它具有无功能驱动程序和没有大写或较低级别的筛选器驱动程序。 Raw 模式的所有 i/o 操作是通过总线驱动程序和可选总线筛选器驱动程序。

 

 




