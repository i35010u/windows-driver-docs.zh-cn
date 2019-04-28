---
title: 电源管理框架概述
description: 从 Windows 8 开始，运行时电源管理框架 (PoFx) 支持组件 （或子） 级别的功能和时钟管理。
ms.assetid: 9F2D8ACD-44D5-46E0-9FC7-1B38B99450FF
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d90b6db0fbbb0ee964a6ed7e9dafdd7a7d2e11d2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352020"
---
# <a name="overview-of-the-power-management-framework"></a>电源管理框架概述


从 Windows 8 开始，运行时电源管理框架 (PoFx) 支持组件 （或子） 级别的功能和时钟管理。 设备驱动程序注册到 PoFx 独立地管理设备中的各个组件中的电源使用情况。 PoFx 提供所需来扩展 Windows 便携式计算机、 平板电脑、 手机或其他移动设备可以在电池电量运行的时间的细粒度控制。 PoFx 减少了维护始终处于打开和始终连接的移动设备的外观的方式的电源使用情况。

组件或子，是起作用的硬件单元可以打开或切换到低功耗状态独立于其他组件在同一设备的设备中。 例如，音频设备可能有单独的组件，供其播放和录制状态可以互相独立地管理其功能。 如果正在使用的播放组件，但录制组件处于空闲状态，录制组件可以切换到低功耗状态而不会干扰播放组件的活动。


 

 




