---
title: 处理电源 IRP 时调用 ExSetTimerResolution
description: 处理电源 IRP 时调用 ExSetTimerResolution
ms.assetid: 999a76ab-1586-4157-bfa7-8cc5dd517c71
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 6192ccde5d916080620a6180b89055adfe6c5aac
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338616"
---
# <a name="calling-exsettimerresolution-while-processing-a-power-irp"></a>处理电源 IRP 时调用 ExSetTimerResolution


在处理期间[ **IRP\_MJ\_POWER** ](https://msdn.microsoft.com/library/windows/hardware/ff550784)请求时，电源管理器持有的锁资源的[ **ExSetTimerResolution** ](https://msdn.microsoft.com/library/windows/hardware/ff545614)必须获取才能完成。 因此，如果驱动程序直接或间接处理 power 请求时调用此例程，然后等待调用例程，以返回在驱动程序完成 power 请求之前，将发生死锁。 在处理 power 请求时，驱动程序可以安全地调用**ExSetTimerResolution**仅当该驱动程序不会等待对此例程的调用返回之前完成 power 请求。 例如，驱动程序可以创建调用的工作线程**ExSetTimerResolution**，只要该驱动程序然后完成电源请求而无需等待对此例程的调用返回。

 

 




