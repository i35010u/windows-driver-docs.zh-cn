---
title: 总线驱动程序的启动顺序
description: 总线驱动程序的启动顺序
ms.assetid: 689746F4-E1A5-40BA-9FC4-29B0702D6E3E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e0a1dbfb78dca14d1ec92e9258f752e78fce8374
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89190323"
---
# <a name="power-up-sequence-for-a-bus-driver"></a>总线驱动程序的启动顺序


下图显示了当设备到完全操作状态时，框架调用 KMDF 总线驱动程序的事件回调函数的顺序，从图底部的设备插入状态开始：

![总线驱动程序的通电顺序](images/pdo-powerup.png)

在物理上将相应的设备从系统中删除之前，框架不会实际删除 PDO。 例如，如果用户在设备管理器中禁用了该设备，但未将其物理删除，则该框架将保留其设备对象。 因此，该图底部的三个步骤仅在即插即用枚举过程中发生，即在初始启动期间或用户插入新设备时。 如果以前禁用了该设备但未将其物理删除，则该框架首先调用 [*EvtDevicePrepareHardware*](/windows-hardware/drivers/ddi/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware) 回调。

 

