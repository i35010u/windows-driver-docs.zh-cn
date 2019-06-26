---
title: 处理 IRP_MN_REGINFO 和 IRP_MN_REGINFO_EX 以注册块
description: 处理 IRP_MN_REGINFO 和 IRP_MN_REGINFO_EX 以注册块
ms.assetid: 2c17fc63-3c33-4d03-8c46-8d56242556d1
keywords:
- WMI WDK 内核，向 WMI 注册
- 注册 WMI 数据提供程序
- 数据提供程序 WDK WMI
- 驱动程序注册 WDK WMI
- 事件阻止 WDK WMI
- 块 WDK WMI
- IRP_MN_REGINFO
- IRP_MN_REGINFO_EX
- 注册块
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: c94475ba7e2d04083170696d23bae618a3d09495
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67383326"
---
# <a name="handling-irpmnreginfo-and-irpmnreginfoex-to-register-blocks"></a>处理 IRP\_MN\_REGINFO 和 IRP\_MN\_REGINFO\_EX 注册块





在 Windows 98 和 Windows 2000 上，系统会发送[ **IRP\_MN\_REGINFO** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo)到驱动程序的请求，以允许注册其 WMI 类的驱动程序。 Windows XP 及更高版本，系统会发送[ **IRP\_MN\_REGINFO\_EX** ](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-reginfo-ex)改为请求。 大多数驱动程序可以处理这些请求通过使用[ **WmiSystemControl** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmilib/nf-wmilib-wmisystemcontrol)可以提供一个回调例程。 请参阅[使用 WMI 库对注册块](using-the-wmi-library-to-register-blocks.md)有关详细信息。

驱动程序必须处理**IRP\_MN\_REGINFO**或**IRP\_MN\_REGINFO\_EX**请求，以注册使用动态的块实例名称，或使用一系列驱动程序定义的静态实例名称;它不能调用**WmiSystemControl**注册此类块。 驱动程序可以根据需要处理此请求以便注册使用基于 PDO 或驱动程序定义的基本名称字符串的静态实例名称的块。

在此情况下，该驱动程序：

1.  填写[ **WMIREGINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-wmireginfow)结构，在**Parameters.WMI.Buffer** ，它指定：

    -   提供的驱动程序，包括代表另一个驱动程序提供数据的所有注册数据的字节数。

    -   驱动程序的注册表路径。

    -   驱动程序的 MOF 资源的名称。

    -   若要注册的块的数目。

    -   一个数组[ **WMIREGGUID** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-wmiregguidw)结构，一个用于每个块。

2.  对于每个块，该驱动程序会填写**WMIREGGUID**结构，它指定：

    -   表示块的 GUID。

    -   提供有关实例名称和其他特征的块的信息，如块是否收集成本很高的标志。 有关详细信息，请参阅[WMI 注册标志](wmi-registration-flags.md)。

    如果使用静态实例名称注册了块，驱动程序设置一个要指定静态实例名称数据块的以下成员：

    -   如果驱动程序设置**标志**与 WMIREG\_标志\_实例\_列表中，设置**InstanceNameList**到一组静态实例名称字符串的偏移量。 WMI 实例在后续请求中通过指定索引到此列表中。

    -   如果驱动程序设置**标志**与 WMIREG\_标志\_实例\_基本名称，它会设置**BaseNameOffset**为偏移量为基名称字符串。 WMI 使用此字符串来生成块的静态实例名称。

    -   如果驱动程序设置**标志**与 WMIREG\_标志\_实例\_PDO，它会设置**Pdo** PDO 到传递给驱动程序的[ *AddDevice* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_add_device)例程。 WMI 使用 PDO 的设备实例路径来生成块的静态实例名称。 在处理时**IRP\_MN\_REGINFO\_EX**请求，驱动程序必须调用[ **ObReferenceObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obfreferenceobject)例程上传入的物理设备对象**Pdo**。 (系统将自动调用[ **ObDereferenceObject** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nf-wdm-obdereferenceobject)若要取消引用的对象; 该驱动程序必须执行此操作。)

    该驱动程序将写入实例名称字符串或所指示的偏移量处的基名称的字符串**InstanceNameList**或**BaseName**分别。

3.  如果驱动程序正在注册块代表另一个驱动程序 （如类驱动程序可能代表 miniclass 驱动程序），该驱动程序在另一个将填充[ **WMIREGINFO** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-wmireginfow)结构和列表[**WMIREGGUID** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wmistr/ns-wmistr-wmiregguidw)结构的其他驱动程序的块的注册信息并设置**NextWmiRegInfo**在第一个**WMIREGINFO**从头到尾的第一个字节的偏移量**WMIREGINFO**到第二个开头**WMIREGINFO**结构。

 

 




