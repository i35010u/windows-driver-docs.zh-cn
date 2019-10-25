---
title: WMI 注册标志
description: WMI 注册标志
ms.assetid: 001d4840-0ed4-464d-8379-7bbd0afce28c
keywords:
- 动态实例名称 WDK WMI
- 静态实例名称 WDK WMI
- 注册标志 WDK WMI
- 标志 WDK WMI
- WMI WDK 内核，用 WMI 注册
- 注册 WMI 数据提供程序
- 数据访问接口 WDK WMI
- 驱动程序注册 WDK WMI
- 事件块 WDK WMI
- 阻止 WDK WMI
- 注册块
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9e8fe309f38ab40c68a2b98f573e9feb59b0e284
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72835654"
---
# <a name="wmi-registration-flags"></a>WMI 注册标志





驱动程序指示块是使用静态还是动态实例名称，并通过在[**WMIGUIDREGINFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmiguidreginfo)或[**WMIREGGUID**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmiregguidw)结构中设置标志并将其传递给 WMI 以注册块来指定块的其他特征。

驱动程序通过设置以下某个标志，指示块使用静态实例名称：

-   WMIREG\_标记\_实例\_列表指示驱动程序提供静态列表中的所有实例名称。

    仅当驱动程序通过处理[**IRP\_MN\_REGINFO**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)或[**IRP\_MN\_REGINFO\_EX**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex)请求，而不是调用[**WmiSystemControl**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)，才能设置此标志。 驱动程序在块的**WMIREGGUID**结构中的**InstanceNameList**指示的字节偏移量处写入实例名称字符串。

-   WMIREG\_标记\_实例\_指示 WMI 从驱动程序定义的基名称字符串生成静态实例名称。

    处理**IRP\_MN\_REGINFO**或**irp\_MN\_REGINFO\_EX**请求的驱动程序在块的**BaseNameOffset**中的**WMIREGGUID**指示的偏移量处写入基名称字符串。构造.

    调用**WmiSystemControl**的驱动程序在其[**DpWmiQueryReginfo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_reginfo_callback)例程的*InstanceName*参数中指定基名称字符串。

-   WMIREG\_标记\_实例\_PDO 指示 WMI 从驱动程序的 PDO 的设备实例 ID 生成静态实例名称。

    处理**IRP\_MN\_REGINFO**或**irp\_MN\_REGINFO\_EX**请求的驱动程序在块的**WMIREGGUID**结构的**pdo**成员上写入一个指向 pdo 的指针。 如果请求为**IRP\_MN\_REGINFO\_EX**，则驱动程序必须在通过调用[**ObReferenceObject**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject)例程传递的每个 PDO 上增加引用计数。 （系统稍后会对每个 PDO 取消引用。）

    调用**WmiSystemControl**的驱动程序会在其[*DpWmiQueryReginfo*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_reginfo_callback)例程的*pdo*参数中写入一个指向 pdo 的指针。

若要指示某个块使用动态实例名称，驱动程序不得设置以下任何标志： WMIREG\_标记\_实例\_列表、WMIREG\_标志\_实例\_PDO 或 WMIREG\_标志\_实例\_BASENAME。

驱动程序表明，通过将\_WMIREG 设置为\_开销，数据块的收集成本高昂。 这会指示 WMI 发送[**IRP\_MN\_** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-enable-collection)在 wmi 客户端第一次打开数据块和 IRP\_MN 时启用\_集合请求，最后一个 wmi 客户端关闭后，将[**禁用\_收集**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-disable-collection)请求块。 驱动程序在接收**IRP\_MN\_启用\_收集**请求之前，不需要为此类块收集数据。

驱动程序通过将 WMIREG\_标志设置为仅\_GUID\_\_事件来指示事件块。 这表示只能将块作为事件启用或禁用，且不能对其进行查询或设置。

驱动程序通过将\_WMIREG 设置为\_删除\_GUID 来指示 WMI 删除以前注册的块。 此标志仅在响应更新注册信息的请求时有效（[**irp\_MN\_REGINFO**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)或[**IRP\_MN\_REGINFO\_EX**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex) with WMIUPDATE）。 有关详细信息，请参阅[更新 WMI 注册信息](updating-wmi-registration-information.md)。

 

 




