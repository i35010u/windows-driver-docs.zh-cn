---
title: 关于 ISensorClassExtension
description: 关于 ISensorClassExtension
ms.date: 07/20/2018
ms.localizationpriority: medium
ms.openlocfilehash: 1a6b78831fe24e31768d6dce7d6a4815581709bd
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96831111"
---
# <a name="about-isensorclassextension"></a>关于 ISensorClassExtension


传感器驱动程序使用 ISensorClassExtension 来初始化和 unitialize 传感器类扩展、引发事件、进程 WPD 输入/输出控制代码 (IOCTLs) 并正确关闭 UMDF 文件句柄。

## <a name="methods-to-manage-object-lifetime"></a>用于管理对象生存期的方法

若要初始化类扩展，基于 PnP 的硬件传感器驱动程序会调用 [**ISensorClassExtension：： initialize**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-initialize) （当 [**IPnpCallbackHardware：： ONPREPAREHARDWARE**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onpreparehardware)中由 UMDF 调用时）。 此步骤为类扩展对象提供指向驱动程序的主类的指针，并为实现回调接口的类提供用于处理类扩展对象所引发的事件的类。 当 [**IPnpCallbackHardware：： OnReleaseHardware**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallbackhardware-onreleasehardware)中的 UMDF 调用驱动程序时，它应调用 [**ISensorClassExtension：：取消初始化**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-uninitialize) ，然后释放类扩展对象。 请注意，某些类型的传感器可能需要在不同时间初始化和取消初始化类扩展。

## <a name="methods-to-raise-events"></a>引发事件的方法

驱动程序可以通过调用 [**ISensorClassExtension：:P oststatechange**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-poststatechange)调用 [**ISensorClassExtension：:P ostevent**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-postevent)和 state information 事件，引发各种传感器事件 (通常包含传感器数据) 。 有关传感器驱动程序中事件的工作原理的详细信息，请参阅 [关于传感器驱动程序事件](about-sensor-driver-events.md)。

## <a name="methods-to-manage-ioctls-and-handles"></a>用于管理 IOCTLs 和句柄的方法

传感器驱动程序将两种 UMDF 调用转发到类扩展：

-   处理通过 [**IQueueCallbackDeviceIoControl：： OnDeviceIoControl**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-iqueuecallbackdeviceiocontrol-ondeviceiocontrol)接收到的 i/o 控制代码的请求。 若要将 i/o 请求转发给类扩展以便进行处理，驱动程序必须调用 [**ISensorClassExtension：:P rocessiocontrol**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-processiocontrol)。

-   有关关闭通过 [**IFileCallbackCleanup：： OnCleanupFile**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ifilecallbackcleanup-oncleanupfile)接收的文件句柄的客户端的通知。 若要转发 i/o 请求取消，驱动程序必须调用 [**ISensorClassExtension：： CleanupFile**](/windows-hardware/drivers/ddi/sensorsclassextension/nf-sensorsclassextension-isensorclassextension-cleanupfile)。

 

