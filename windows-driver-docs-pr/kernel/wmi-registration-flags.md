---
title: WMI 注册标志
description: WMI 注册标志
ms.assetid: 001d4840-0ed4-464d-8379-7bbd0afce28c
keywords:
- 动态实例名称 WDK WMI
- 静态实例名称 WDK WMI
- 注册标记 WDK WMI
- 标志 WDK WMI
- WMI WDK 内核，向 WMI 注册
- 注册 WMI 数据提供程序
- 数据提供程序 WDK WMI
- 驱动程序注册 WDK WMI
- 事件阻止 WDK WMI
- 块 WDK WMI
- 注册块
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: dfae2587cb8e93195053bb50c727caca34a74bc2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63327232"
---
# <a name="wmi-registration-flags"></a>WMI 注册标志





驱动程序指示应用程序块使用静态还是动态实例名称，并通过设置标志指定块的其他特征[ **WMIGUIDREGINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff565811)或[ **WMIREGGUID** ](https://msdn.microsoft.com/library/windows/hardware/ff565827)结构将传递到 WMI，以注册该块。

驱动程序指示块通过设置以下标志之一来使用静态实例名称：

-   WMIREG\_标志\_实例\_列表指示驱动程序提供了所有实例的静态列表中的名称。

    驱动程序可以设置此标志仅当它通过处理注册块[ **IRP\_MN\_REGINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551731)或者[ **IRP\_MN\_REGINFO\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff551734)请求，不是通过调用[ **WmiSystemControl**](https://msdn.microsoft.com/library/windows/hardware/ff565834)。 该驱动程序将实例写入所指示的字节偏移量处的名称字符串**InstanceNameList**中的块**WMIREGGUID**结构。

-   WMIREG\_标志\_实例\_BASENAME 指示 WMI 可从驱动程序定义的基本名称字符串生成静态实例的名称。

    处理的驱动程序**IRP\_MN\_REGINFO**或**IRP\_MN\_REGINFO\_EX**请求写入处的基名称字符串由指示偏移量**BaseNameOffset**中的块**WMIREGGUID**结构。

    调用的驱动程序**WmiSystemControl**指定的基名称字符串*InstanceName*参数及其[ **DpWmiQueryReginfo** ](https://msdn.microsoft.com/library/windows/hardware/ff544097)例程。

-   WMIREG\_标志\_实例\_PDO 指示 WMI 可从设备实例 ID 的驱动程序的 PDO 生成静态实例的名称。

    处理的驱动程序**IRP\_MN\_REGINFO**或**IRP\_MN\_REGINFO\_EX**请求将一个指针，写入到在PDO**Pdo**的块的成员**WMIREGGUID**结构。 该请求是否**IRP\_MN\_REGINFO\_EX**，该驱动程序必须增加传递通过调用每个 PDO 的引用计数[ **ObReferenceObject**](https://msdn.microsoft.com/library/windows/hardware/ff558678)例程。 （系统将取消引用每个 PDO 更高版本。）

    调用的驱动程序**WmiSystemControl**指针写入在 PDO *Pdo*参数及其[ *DpWmiQueryReginfo* ](https://msdn.microsoft.com/library/windows/hardware/ff544097)例程。

若要指示一个块，使用动态实例名称，该驱动程序必须不设置任何下列标志：WMIREG\_标志\_实例\_列表中，WMIREG\_标志\_实例\_PDO 或 WMIREG\_标志\_实例\_BASENAME。

驱动程序指示数据块是相当昂贵收集通过设置 WMIREG\_标志\_昂贵。 这会指示 WMI 发送[ **IRP\_MN\_启用\_集合**](https://msdn.microsoft.com/library/windows/hardware/ff550857)请求第一次 WMI 客户端打开数据块和一个[ **IRP\_MN\_禁用\_集合**](https://msdn.microsoft.com/library/windows/hardware/ff550848)时最后一个 WMI 客户端关闭块请求。 该驱动程序需要不会收集此类块的数据，直到收到**IRP\_MN\_启用\_集合**请求。

驱动程序通过设置 WMIREG 来指示事件块\_标志\_事件\_仅\_GUID。 这表示块可以启用或禁用了作为事件，并不能查询或设置。

驱动程序将指示 WMI 删除以前已注册的块通过设置 WMIREG\_标志\_删除\_GUID。 此标志是仅在响应请求来更新注册信息中有效 ([**IRP\_MN\_REGINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551731)或者[ **IRP\_MN\_REGINFO\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff551734)与 WMIUPDATE)。 有关详细信息，请参阅[更新 WMI 注册信息](updating-wmi-registration-information.md)。

 

 




