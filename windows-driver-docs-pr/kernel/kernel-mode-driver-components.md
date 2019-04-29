---
title: 内核模式驱动程序组件
description: 内核模式驱动程序组件
ms.assetid: 79be2948-cc74-4f0b-8ffa-1e57f44d7b0c
keywords:
- 内核模式驱动程序 WDK，组件
- 内核模式驱动程序 WDK，标准驱动程序例程
- 标准驱动程序例程 WDK 内核
- 驱动程序例程 WDK 内核
- 例程 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4658ce73b6ae6d7d6cf68dd56c6e7f35ed0e2456
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63381383"
---
# <a name="kernel-mode-driver-components"></a>内核模式驱动程序组件





本部分介绍内核模式驱动程序中包含的标准例程。 其中一些*标准驱动程序例程*是必需的; 其他为可选。 本部分还介绍了*驱动程序对象*，其中包含指向每个驱动程序的标准例程的指针。

某些驱动程序与系统提供的端口驱动程序或定义很多驱动程序的所需的功能的类驱动程序进行交互。 例如，SCSI 微型端口驱动程序主要使用 SCSI 端口驱动程序交互。 此类驱动程序，请参阅必选和可选驱动程序支持的详细信息的特定于类的文档。

本部分包括：

[标准驱动程序例程简介](introduction-to-standard-driver-routines.md)

[标准驱动程序的常规要求](standard-driver-routine-requirements.md)

[驱动程序对象简介](introduction-to-driver-objects.md)

[编写 DriverEntry 例程](writing-a-driverentry-routine.md)

[写入一个重新初始化例程](writing-a-reinitialize-routine.md)

[编写 AddDevice 例程](writing-an-adddevice-routine.md)

[写入调度例程](writing-dispatch-routines.md)

[编写卸载例程](writing-an-unload-routine.md)

 

 




