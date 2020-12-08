---
title: 供应商扩展的事件
description: 供应商扩展的事件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: eaf8320d149526514f95963fecc4da596f19a80b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822345"
---
# <a name="vendor-extended-events"></a>供应商扩展的事件





供应商扩展事件在 **DeviceData** 和 **events** INF 文件部分中定义 (参阅 [供应商扩展功能](vendor-extended-features.md)) 中的示例。 **EventCode** 条目列出了以逗号分隔的所有事件代码。 对于每个事件代码，应存在一个 **EventCode**_XXXX_ 形式的条目，其中 XXXX 是大写十六进制形式的 PTP 事件代码。 当驱动程序收到事件代码时，条目应列出要发送的 WIA GUID 代码。

事件的显示名称应在 **events** 节中声明。 对于每个事件，必须有一个 **EventCode**_XXXX_ 条目，其中包含引号中的事件名称、事件 GUID，以及事件发生时要启动的应用程序，所有这些事件都由逗号分隔。 如果使用星号代替应用程序名称，则使用已注册的应用程序名称。 有关详细信息，请参阅 [WIA 设备的 INF 文件](inf-files-for-wia-devices.md) 。 应用程序可以使用 **IWiaDevMgr：： RegisterEventCallback**_Xxx_ 方法 (Microsoft Windows SDK 文档) 中所述的方法来接收事件。 当前无法将事件中的参数传递给应用程序。

 

 




