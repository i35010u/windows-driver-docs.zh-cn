---
description: 要求
title: 要求
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c4e67a06c61009aa97d4d3cfc287a9cfc4cf1976
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969472"
---
# <a name="requirements"></a>要求


若要创建 (WPD) 驱动程序的 Windows 便携式设备，你的计算机上必须安装最新的 [Windows 驱动程序工具包 (WDK) ](https://go.microsoft.com/fwlink/p/?linkid=178709) 。 以下列表中显示了所需的标头文件和库文件，并且这些文件包含在 WDK 中：

-   *PortableDeviceGuids*
-   *PortableDeviceClassExtension*
-   *PortableDeviceTypes*
-   *PortableDevice*
-   用户模式驱动程序框架所需的任何其他所需的库或标头文件 (UMDF) 。

如果你的驱动程序支持新的设备服务模型，它还将包括一个或多个以下标头文件：

-   *AnchorSyncDeviceService*
-   *BridgeDeviceService*
-   *CalendarDeviceService*
-   *ContactDeviceService*
-   *DeviceServices*
-   *FullEnumSyncDeviceService*
-   *HintsDeviceService*
-   *MessageDeviceService*
-   *MetadataDeviceService*
-   *NotesDeviceService*
-   *RingtoneDeviceService*
-   *StatusDeviceService*
-   *SyncDeviceService*
-   *TaskDeviceService*

在这些文件中，所有服务应用程序都需要 *BridgeDeviceService* 和 *DeviceService* 。 其他应用程序必须包括一个或多个其他文件以支持特定设备。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**WPD 驱动程序**](wpd-drivers.md)

 

 





