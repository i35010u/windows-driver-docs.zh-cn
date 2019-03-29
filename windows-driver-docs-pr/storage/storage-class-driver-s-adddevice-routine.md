---
title: 存储类驱动程序的 AddDevice 例程
description: 存储类驱动程序的 AddDevice 例程
ms.assetid: ff07ae84-2748-44b4-88c6-e67f1d4c9268
keywords:
- AddDevice 例程 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b21dd6bc0184bbb64dded884b35d72655f0b353
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56563697"
---
# <a name="storage-class-drivers-adddevice-routine"></a>存储类驱动程序的 AddDevice 例程


## <span id="ddk_storage_class_drivers_adddevice_routine_kg"></span><span id="DDK_STORAGE_CLASS_DRIVERS_ADDDEVICE_ROUTINE_KG"></span>


PnP 管理器中调用存储类驱动程序的[ **AddDevice** ](https://msdn.microsoft.com/library/windows/hardware/ff540521)例程时检测到由该驱动程序控制的设备。 存储类驱动程序的*AddDevice*例程：

-   声明该设备，如中所述[存储类驱动程序 ClaimDevice 例程](storage-class-driver-s-claimdevice-routine.md)，或如果该驱动程序不能声明设备，将返回状态\_成功。

-   如果该驱动程序已成功对声明该设备，将创建一个设备对象 (FDO)。

-   注册应用程序和其他系统设备可以使用的设备接口。 接收即插即用启动请求时，类驱动程序将使此类接口。

-   准备要处理一个开始请求中所述的设备对象[编写 AddDevice 例程](https://msdn.microsoft.com/library/windows/hardware/ff566398)。

-   通过调用将设备对象附加到设备堆栈[ **IoAttachDeviceToDeviceStack** ](https://msdn.microsoft.com/library/windows/hardware/ff548300) PDO 中的输入。

-   如果设备在已知的电源状态启动，则调用[ **PoSetPowerState**](https://msdn.microsoft.com/library/windows/hardware/ff559765)。

-   清除 DO\_设备\_正在初始化新的设备对象上的标志。

存储类驱动程序将存储返回的指针**IoAttachDeviceToDeviceStack**在其自己设备 (FDO) 对象，该对象表示已声明新的设备，设备扩展和*必须在所有使用此指针在类驱动程序将发送到下一步低驱动程序的后续请求*。 该驱动程序还将对输入 PDO 指针存储在设备扩展，但在**IoAttachDeviceToDeviceStack**返回驱动程序必须使用仅在调用即插即用中的输入 PDO 指向 **Io * * * Xxx*获得此类指针作为参数的例程。

有关详细信息，请参阅[编写 AddDevice 例程](https://msdn.microsoft.com/library/windows/hardware/ff566398)。

 

 




