---
title: 总线驱动程序的启动顺序
description: 总线驱动程序的启动顺序
ms.assetid: 689746F4-E1A5-40BA-9FC4-29B0702D6E3E
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 27d2919a7aae5b8058417308fd5bd8ad85a1581c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543021"
---
# <a name="power-up-sequence-for-a-bus-driver"></a>总线驱动程序的启动顺序


下图显示了使设备为完全可操作的状态，从该图底部的设备插入状态时框架调用 KMDF 总线驱动程序的事件回调函数的顺序：

![总线驱动程序的启动顺序](images/pdo-powerup.png)

框架不会以物理方式删除 PDO 之前以物理方式从系统中删除相应的设备。 例如，如果用户禁用的设备在设备管理器，但不会以物理方式删除它，该框架将保留其设备对象。 因此，仅在插枚举时发生图底部的三个步骤 — 即，在初始启动或在用户插入新设备。 如果设备已之前处于禁用状态，但不是以物理方式删除，framework 将先通过调用[ *EvtDevicePrepareHardware* ](https://msdn.microsoft.com/library/windows/hardware/ff540880)回调。

 

 





