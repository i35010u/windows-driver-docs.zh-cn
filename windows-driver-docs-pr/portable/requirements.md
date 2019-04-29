---
Description: 要求
title: 要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 65cfd58a71c6da5af4bfed01d51d8a48bc9b1835
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376223"
---
# <a name="requirements"></a>要求


若要创建 Windows 便携式设备 (WPD) 驱动程序，必须具有最新[Windows Driver Kit (WDK)](https://go.microsoft.com/fwlink/p/?linkid=178709)在计算机上安装。 所需的标头和库文件在以下列表中所示，WDK 中包含：

-   *PortableDeviceGuids.lib*
-   *PortableDeviceClassExtension.h*
-   *PortableDeviceTypes.h*
-   *PortableDevice.h*
-   任何其他所需的库或所需的用户模式驱动程序框架 (UMDF) 的标头文件。

如果您的驱动程序支持新的设备服务模型，它还将包括一个或多个以下的标头文件：

-   *AnchorSyncDeviceService.h*
-   *BridgeDeviceService.h*
-   *CalendarDeviceService.h*
-   *ContactDeviceService.h*
-   *DeviceServices.h*
-   *FullEnumSyncDeviceService.h*
-   *HintsDeviceService.h*
-   *MessageDeviceService.h*
-   *MetadataDeviceService.h*
-   *NotesDeviceService.h*
-   *RingtoneDeviceService.h*
-   *StatusDeviceService.h*
-   *SyncDeviceService.h*
-   *TaskDeviceService.h*

这些文件的*BridgeDeviceService.h*并*DeviceService.h*所需的所有服务应用程序。 其他应用程序必须包含一个或多个这些其他文件，以支持特定的设备。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**WPD 驱动程序**](wpd-drivers.md)

 

 





