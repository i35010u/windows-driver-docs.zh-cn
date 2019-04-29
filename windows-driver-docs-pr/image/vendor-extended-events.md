---
title: 供应商扩展的事件
description: 供应商扩展的事件
ms.assetid: 00131b75-3b15-46f8-b4da-1e1593afb3c0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56633f19d0b82b1f2a2db7d3078e1ead510555d2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356127"
---
# <a name="vendor-extended-events"></a>供应商扩展的事件





供应商扩展事件中定义**DeviceData**并**事件**INF 文件部分 (请参阅中的示例[Vendor-Extended 功能](vendor-extended-features.md))。 **EventCode**项列出了所有事件代码，以逗号隔开。 对于每个事件代码，窗体的一个条目 **EventCode * * * XXXX*应存在，其中 XXXX 是 PTP 事件代码以大写十六进制格式。 该条目应列出 WIA GUID 代码以发送由驱动程序收到的事件代码。

应在声明事件的显示名称**事件**部分。 对于每个事件，必须有 **EventCode * * * XXXX*包含引号、 GUID、 事件和事件发生时，启动的应用程序中的事件名称的条目，所有通过以逗号分隔。 如果星号代替应用程序名称，则使用注册的应用程序名称。 请参阅[WIA 设备 INF 文件](inf-files-for-wia-devices.md)有关详细信息。 应用程序可以使用 **IWiaDevMgr::RegisterEventCallback * * * Xxx* （Microsoft Windows SDK 文档中所述） 方法以将事件接收。 目前，从该事件的参数不能传递到应用程序。

 

 




