---
title: WMI 注册标志
description: WMI 注册标志
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
ms.openlocfilehash: 7896813d0e852cdadbbc252eca795ed1aa36fde3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782645"
---
# <a name="wmi-registration-flags"></a>WMI 注册标志





驱动程序指示块是使用静态还是动态实例名称，并通过在 [**WMIGUIDREGINFO**](/windows-hardware/drivers/ddi/wmilib/ns-wmilib-_wmiguidreginfo) 或 [**WMIREGGUID**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmiregguidw) 结构中设置标志并将其传递给 WMI 以注册块来指定块的其他特征。

驱动程序通过设置以下某个标志，指示块使用静态实例名称：

-   WMIREG \_ 标记 \_ 实例 \_ 列表指示驱动程序提供静态列表中的所有实例名称。

    仅当驱动程序通过处理 [**IRP \_ MN \_ REGINFO**](./irp-mn-reginfo.md) 或 [**irp \_ MN \_ REGINFO \_ EX**](./irp-mn-reginfo-ex.md) 请求（而不是调用 [**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol)）来注册阻止时，才可以设置此标志。 驱动程序在块的 **WMIREGGUID** 结构中的 **InstanceNameList** 指示的字节偏移量处写入实例名称字符串。

-   WMIREG \_ 标记 \_ 实例 \_ BASENAME 指示 WMI 从驱动程序定义的基名称字符串生成静态实例名称。

    处理 **IRP \_ MN \_ REGINFO** 或 **irp \_ MN \_ REGINFO \_ EX** 请求的驱动程序会在块的 **BaseNameOffset** 结构中用 **WMIREGGUID** 指示的偏移量写入基名称字符串。

    调用 **WmiSystemControl** 的驱动程序在其 [**DpWmiQueryReginfo**](/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_reginfo_callback)例程的 *InstanceName* 参数中指定基名称字符串。

-   WMIREG \_ 标志 \_ 实例 \_ PDO 指示 WMI 从驱动程序 PDO 的设备实例 ID 生成静态实例名称。

    处理 **IRP \_ MN \_ REGINFO** 或 **irp \_ MN \_ REGINFO \_ EX** 请求的驱动程序在块的 **WMIREGGUID** 结构的 **pdo** 成员上写入一个指向 pdo 的指针。 如果请求为 **IRP \_ MN \_ REGINFO \_ EX**，则驱动程序必须在通过调用 [**OBREFERENCEOBJECT**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject) 例程传递的每个 PDO 上增加引用计数。  (系统稍后将取消引用每个 PDO。 ) 

    调用 **WmiSystemControl** 的驱动程序会在其 [*DpWmiQueryReginfo*](/windows-hardware/drivers/ddi/wmilib/nc-wmilib-wmi_query_reginfo_callback)例程的 *pdo* 参数中写入一个指向 pdo 的指针。

若要指示某个块使用动态实例名称，驱动程序不得设置以下任何标志： WMIREG \_ 标记 \_ 实例 \_ 列表、WMIREG \_ 标记 \_ 实例 \_ PDO 或 WMIREG \_ 标志 \_ 实例 \_ BASENAME。

驱动程序指示通过设置 WMIREG 标志昂贵来收集数据块的成本很高 \_ \_ 。 这会指示 WMI 在第一次打开数据块时，发送 [**irp \_ MN \_ ENABLE \_ collection**](./irp-mn-enable-collection.md) 请求，当最后一个 wmi 客户端关闭块时，将使用 [**IRP \_ MN \_ 禁用 \_ 集合**](./irp-mn-disable-collection.md) 请求。 驱动程序无需在收到 **IRP \_ MN \_ ENABLE \_ COLLECTION** 请求之前收集此类数据。

驱动程序通过设置 WMIREG \_ 标志 \_ \_ 仅事件 GUID 来指示事件块 \_ 。 这表示只能将块作为事件启用或禁用，且不能对其进行查询或设置。

驱动程序通过设置 WMIREG \_ 标志删除 GUID 来指示 WMI 删除以前注册的块 \_ \_ 。 此标志仅在响应 ([**IRP \_ MN \_ REGINFO**](./irp-mn-reginfo.md) 或 [**IRP \_ MN \_ REGINFO \_ EX**](./irp-mn-reginfo-ex.md) with WMIUPDATE) 的更新注册信息的请求时有效。 有关详细信息，请参阅 [更新 WMI 注册信息](updating-wmi-registration-information.md)。

 

