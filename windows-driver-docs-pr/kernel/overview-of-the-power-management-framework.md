---
title: 电源管理框架概述
description: 从 Windows 8 开始，运行时电源管理框架 (PoFx) 支持组件 (或 subdevice) 级别的电源和时钟管理。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: eb72bbbaf086a63bda9945d311a9352e10be371e
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788593"
---
# <a name="overview-of-the-power-management-framework"></a>电源管理框架概述


从 Windows 8 开始，运行时电源管理框架 (PoFx) 支持组件 (或 subdevice) 级别的电源和时钟管理。 设备驱动程序将注册到 PoFx，以独立管理设备中单个组件的电源使用情况。 PoFx 提供所需的精细控制，以延长 Windows 便携式计算机、平板电脑、手机或其他移动设备在电池电量上运行的时间。 PoFx 降低了电源使用情况，该方法可保持始终开机和始终连接的移动设备的外观。

组件（或 subdevice）是设备中的一种功能硬件单元，可以在同一设备中独立于其他组件打开或切换到低功耗状态。 例如，音频设备可能具有不同的播放和记录组件，其电源状态可以彼此独立地进行管理。 如果正在使用播放组件，但记录组件处于空闲状态，则可以将记录组件切换到低功耗状态，而不会干扰播放组件的活动。


 

 




