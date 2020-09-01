---
title: 处理 IRP_MN_REGINFO 和 IRP_MN_REGINFO_EX 以注册块
description: 处理 IRP_MN_REGINFO 和 IRP_MN_REGINFO_EX 以注册块
ms.assetid: 2c17fc63-3c33-4d03-8c46-8d56242556d1
keywords:
- WMI WDK 内核，用 WMI 注册
- 注册 WMI 数据提供程序
- 数据访问接口 WDK WMI
- 驱动程序注册 WDK WMI
- 事件块 WDK WMI
- 阻止 WDK WMI
- IRP_MN_REGINFO
- IRP_MN_REGINFO_EX
- 注册块
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1cb6de6e1ba285f184f34025a135a9023e8e69e0
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188283"
---
# <a name="handling-irp_mn_reginfo-and-irp_mn_reginfo_ex-to-register-blocks"></a>处理 IRP \_ MN \_ REGINFO 和 irp \_ MN \_ REGINFO \_ EX to Register 块





在 Windows 98 和 Windows 2000 上，系统将 [**IRP \_ MN \_ REGINFO**](./irp-mn-reginfo.md) 请求发送到驱动程序，以允许驱动程序注册其 WMI 类。 在 Windows XP 和更高版本中，系统改为发送 [**IRP \_ MN \_ REGINFO \_ EX**](./irp-mn-reginfo-ex.md) 请求。 大多数驱动程序可以通过使用 [**WmiSystemControl**](/windows-hardware/drivers/ddi/wmilib/nf-wmilib-wmisystemcontrol) 来提供回调例程来处理这些请求。 有关详细信息，请参阅 [使用 WMI 库注册块](using-the-wmi-library-to-register-blocks.md) 。

驱动程序必须处理 **irp \_ MN \_ REGINFO** 或 **irp \_ MN \_ REGINFO \_ EX** 请求来注册使用动态实例名称或使用驱动程序定义的静态实例名称列表的块; 它不能调用 **WmiSystemControl** 来注册此类块。 驱动程序可以选择处理此请求，以使用基于 PDO 或驱动程序定义的基名称字符串的静态实例名称注册块。

在这种情况下，驱动程序：

1.  在[**WMIREGINFO**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmireginfow)结构中填充指定**Parameters.WMI.Buffer** ：

    -   驱动程序提供的所有注册数据的字节数，包括代表另一驱动程序提供的数据。

    -   驱动程序的注册表路径。

    -   驱动程序的 MOF 资源的名称。

    -   要注册的块数。

    -   [**WMIREGGUID**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmiregguidw)结构的数组，每个块各有一个。

2.  对于每个块，驱动程序将填充指定以下内容的 **WMIREGGUID** 结构：

    -   表示块的 GUID。

    -   提供有关块的实例名称和其他特性的信息的标志，例如是否收集块很昂贵。 有关详细信息，请参阅 [WMI 注册标志](wmi-registration-flags.md)。

    如果正在向静态实例名称注册块，驱动程序将设置以下成员之一来指定块的静态实例名称数据：

    -   如果驱动程序使用**Flags** WMIREG \_ 标志 \_ 实例列表设置标志 \_ ，则它会将**InstanceNameList**设置为静态实例名称字符串列表的偏移量。 WMI 通过索引向此列表指定后续请求中的实例。

    -   如果驱动程序使用**Flags** WMIREG \_ 标志 \_ 实例 BASENAME 设置标志 \_ ，则它会将**BaseNameOffset**设置为基名称字符串的偏移量。 WMI 使用此字符串生成块的静态实例名称。

    -   如果驱动程序通过**Flags** WMIREG \_ 标志 \_ 实例 PDO 设置标志 \_ ，则会将**pdo**设置为传递给驱动程序的[*AddDevice*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_add_device)例程的 pdo。 WMI 使用 PDO 的设备实例路径为块生成静态实例名称。 处理**IRP \_ MN \_ REGINFO \_ EX**请求时，驱动程序必须在通过**Pdo**传递的物理设备对象上调用[**ObReferenceObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obfreferenceobject)例程。  (系统将自动调用 [**ObDereferenceObject**](/windows-hardware/drivers/ddi/wdm/nf-wdm-obdereferenceobject) ，以取消对对象的引用;该驱动程序不能执行此操作。 ) 

    驱动程序将实例名称字符串或基名称字符串分别写入 **InstanceNameList** 或 **BaseName**所指示的偏移量。

3.  如果驱动程序代表另一个驱动程序注册块 (作为类驱动程序可以代表 miniclass 驱动程序的驱动程序) ，则驱动程序将使用其他驱动程序块的注册信息填充另一[**WMIREGINFO**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmireginfow)结构和[**WMIREGGUID**](/windows-hardware/drivers/ddi/wmistr/ns-wmistr-wmiregguidw)结构列表，并将第一个**WMIREGINFO**中的**NextWmiRegInfo**设置为**从第一个 WMIREGINFO 开始**到第二个**WMIREGINFO**结构开始的偏移量（以字节为单位）。

 

