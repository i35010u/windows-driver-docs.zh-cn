---
title: 总线驱动程序的启动顺序
description: 总线驱动程序的启动顺序
ms.assetid: 689746F4-E1A5-40BA-9FC4-29B0702D6E3E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab08649508a423ec91e9043241be26512a451d67
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67376330"
---
# <a name="power-up-sequence-for-a-bus-driver"></a>总线驱动程序的启动顺序


下图显示了使设备为完全可操作的状态，从该图底部的设备插入状态时框架调用 KMDF 总线驱动程序的事件回调函数的顺序：

![总线驱动程序的启动顺序](images/pdo-powerup.png)

框架不会以物理方式删除 PDO 之前以物理方式从系统中删除相应的设备。 例如，如果用户禁用的设备在设备管理器，但不会以物理方式删除它，该框架将保留其设备对象。 因此，仅在插枚举时发生图底部的三个步骤 — 即，在初始启动或在用户插入新设备。 如果设备已之前处于禁用状态，但不是以物理方式删除，framework 将先通过调用[ *EvtDevicePrepareHardware* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdfdevice/nc-wdfdevice-evt_wdf_device_prepare_hardware)回调。

 

 





