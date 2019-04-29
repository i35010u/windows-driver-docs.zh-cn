---
title: 管理单个设备的电源
description: 管理单个设备的电源
ms.assetid: 95c7e900-5d51-4eb7-8780-1c40befa3599
keywords:
- 电源管理 WDK 内核，设备管理
- 设备电源管理 WDK 内核
- 系统电源状态 WDK 内核
- 节省电源 WDK 内核
- 更改电源状态 WDK 内核
- Irp WDK 电源管理
- I/O 请求数据包 WDK 电源管理
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9d7df6d5266e19b0d8cde98506123533e13183eb
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380265"
---
# <a name="managing-power-for-individual-devices"></a>管理单个设备的电源





驱动程序管理为其设备能力回应[系统电源状态](system-power-states.md)更改检测和关闭空闲状态的设备，并在需要时启动设备。

本部分介绍与设备电源管理相关的以下主题：

[设备的电源状态](device-power-states.md)

[检测空闲设备](detecting-an-idle-device.md)

[管理设备的电源策略](managing-device-power-policy.md)

[处理 IRP\_MN\_设置\_的电源可用于设备的电源状态](handling-irp-mn-set-power-for-device-power-states.md)

[处理 IRP\_MN\_查询\_的电源可用于设备的电源状态](handling-irp-mn-query-power-for-device-power-states.md)

[发送 IRP\_MN\_查询\_电源或 IRP\_MN\_设置\_的电源可用于设备的电源状态](sending-irp-mn-query-power-or-irp-mn-set-power-for-device-power-states.md)

[检测空闲设备](detecting-an-idle-device.md)

[在驱动程序支持 D3cold](supporting-d3cold-in-a-driver.md)

 

 




