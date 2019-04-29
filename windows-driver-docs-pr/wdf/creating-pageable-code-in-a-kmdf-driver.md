---
title: 在 KMDF 驱动程序中创建可分页的代码
description: 在 KMDF 驱动程序中创建可分页的代码
ms.assetid: 5c694ae2-2a16-4c2f-84b0-62e26f4121bc
keywords:
- 可分页的驱动程序 WDK KMDF
- KMDF WDK，可分页的驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0984215e80be19dca7079e6c595cbf25c04bbca9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63392697"
---
# <a name="creating-pageable-code-in-a-kmdf-driver"></a>在 KMDF 驱动程序中创建可分页的代码


*可分页代码*是未使用代码时可以写入到计算机的分页文件的代码。 您可使您的驱动程序部分，以减少其映像加载和初始加载时间并减少使用计算机的有限的非分页的内存池的驱动程序的代码的可分页。

为了帮助您确定是否适合您的驱动程序的可分页的代码或数据，执行以下操作：

1.  识别驱动程序中的可分页部分。

    可分页部分未加载到内存中，直到需要它们。 有关如何在一个驱动程序中创建可分页部分的信息，请参阅[使驱动程序可分页](https://msdn.microsoft.com/library/windows/hardware/ff554346)。

2.  请确保分页驱动程序代码不会影响计算机的功能快速唤醒从低功耗状态。

    驱动程序提供的所有设备对象的回调函数都调用在 IRQL = 被动\_级别，这样就可以提高其代码的可分页 (如中所述[使驱动程序可分页](https://msdn.microsoft.com/library/windows/hardware/ff554346))。

    但是，不应造成会回调函数的代码可分页，如果设备离开低功耗状态，并返回到其工作 (D0) 状态时，框架将调用的回调函数。

    如果此类代码可分页，代码可能会写入到分页文件之前在计算机进入睡眠状态。 因此，计算机会变慢来唤醒因为无法重新加载您的代码 （并因此你的设备不能成为完全可操作） 直到还原分页磁盘的能力。

    因此，回调函数中列出[设备返回到工作状态](a-device-returns-to-its-working-state.md)主题不应为可分页。

3.  确定您的驱动程序需要的驱动程序，例如文件、 注册表中，外部的可分页数据的访问权限还是 power 进行转换时分页池。

    有关如何启用和禁用的驱动程序能够访问 power 转换期间的可分页数据的信息，请参阅[ **WdfDeviceInitSetPowerPageable** ](https://msdn.microsoft.com/library/windows/hardware/ff546766)并[ **WdfDeviceInitSetPowerNotPageable**](https://msdn.microsoft.com/library/windows/hardware/ff546147)。

    有关如何确定您的驱动程序何时在分页状态的信息，请参阅[ **WdfDevStateIsNP**](https://msdn.microsoft.com/library/windows/hardware/ff546958)。

 

 





