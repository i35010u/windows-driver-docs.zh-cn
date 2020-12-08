---
title: 内核模式驱动程序组件
description: 内核模式驱动程序组件
keywords:
- 内核模式驱动程序 WDK，组件
- 内核模式驱动程序 WDK，标准驱动程序例程
- 标准驱动程序例程 WDK 内核
- 驱动程序例程 WDK 内核
- 例程的 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: bd4382e9bc01751c2bdd64e51a58af5d26bdbea3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96806213"
---
# <a name="kernel-mode-driver-components"></a>内核模式驱动程序组件





本部分介绍内核模式驱动程序中包含的标准例程。 其中一些 *标准驱动程序例程* 是必需的;其他选项是可选的。 节还介绍了 *驱动程序对象*，其中包含指向每个驱动程序的标准例程的指针。

某些驱动程序与系统提供的、用于定义驱动程序所需的大部分功能的端口驱动程序或类驱动程序交互。 例如，SCSI 微型端口驱动程序主要与 SCSI 端口驱动程序交互。 有关此类驱动程序的详细信息，请参阅特定于类的文档，以了解必需和可选的驱动程序支持。

本节包括：

[标准驱动程序例程简介](introduction-to-standard-driver-routines.md)

[标准驱动程序例程要求](standard-driver-routine-requirements.md)

[驱动程序对象简介](introduction-to-driver-objects.md)

[编写 DriverEntry 例程](writing-a-driverentry-routine.md)

[编写 Reinitialize 例程](writing-a-reinitialize-routine.md)

[编写 AddDevice 例程](writing-an-adddevice-routine.md)

[编写 Dispatch 例程](writing-dispatch-routines.md)

[编写 Unload 例程](writing-an-unload-routine.md)

 

 




