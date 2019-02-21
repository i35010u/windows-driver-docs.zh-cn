---
title: IoTimer 例程
description: IoTimer 例程
ms.assetid: bc69c7b5-ce63-435e-b5b4-0d65ee153d31
keywords:
- 同步 WDK 内核计时器
- IoTimer
- 设备超时 WDK 内核
- 超时 WDK 内核
- 计时操作 WDK 内核
- 超时设备 I/O 操作 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2c3ad5b26b6efa779b70582c7106dab9b1964c8c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546231"
---
# <a name="iotimer-routines"></a>IoTimer 例程





需要定期调用以确定是否设备操作已超时，更新 （如计数器），某些驱动程序定义的变量或时间的较短时间的时间间隔，则不需要任何操作的驱动程序可以使用[ *IoTimer* ](https://msdn.microsoft.com/library/windows/hardware/ff550381)例程。 *IoTimer*例程是实际的 DPC 例程与 I/O 管理器调用一次每秒的设备对象相关联。 驱动程序可以具有*IoTimer*例行为它创建每个设备对象。

一般情况下，驱动程序应使用*IoTimer*例程需要固定的一秒时间间隔时操作。 需要变量时操作的时间间隔或短于一次每秒的时间间隔，驱动程序应分配计时器对象。 有关详细信息，请参阅[计时器对象和 dpc 进行标记](timer-objects-and-dpcs.md)。

本部分包含以下主题：

[注册和启用 IoTimer 例程](registering-and-enabling-an-iotimer-routine.md)

[提供 IoTimer 上下文信息](providing-iotimer-context-information.md)

[使用 IoTimer 例程](using-an-iotimer-routine.md)

 

 




