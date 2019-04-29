---
title: 更新 WMI 注册信息
description: 更新 WMI 注册信息
ms.assetid: d24688e5-bb50-4bce-a4d4-4a3bf886f86d
keywords:
- WMI WDK 内核，向 WMI 注册
- 注册 WMI 数据提供程序
- 数据提供程序 WDK WMI
- 驱动程序注册 WDK WMI
- 事件阻止 WDK WMI
- 块 WDK WMI
- 注册块
- 更新 WMI 注册信息
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 67ab688a5299ac20a91de68e450c80bf62322dde
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355279"
---
# <a name="updating-wmi-registration-information"></a>更新 WMI 注册信息





其初始注册后使用 WMI，驱动程序更改其注册信息通过调用[ **IoWMIRegistrationControl** ](https://msdn.microsoft.com/library/windows/hardware/ff550480)与以下操作之一：

-   WMIREG\_操作\_重新注册来替换以前提供的驱动程序和新的信息的所有注册信息。

    在响应中，WMI 将发送任一[ **IRP\_MN\_REGINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551731)请求或[ **IRP\_MN\_REGINFO\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff551734)与该驱动程序请求**Parameters.WMI.DataPath**设置为 WMIREGISTER。 (在 Windows 98 和 Windows 2000 上，系统会发送**IRP\_MN\_REGINFO**请求。 在 Windows XP 和更高版本，系统会发送**IRP\_MN\_REGINFO\_EX**请求。)

    驱动程序提供 WMI 使用新的注册信息的所有会阻止该支持，如中所述[使用 WMI 库对注册块](using-the-wmi-library-to-register-blocks.md)并[处理 IRP\_MN\_REGINFO 和 IRP\_MN\_REGINFO\_EX 注册块](handling-irp-mn-reginfo-and-irp-mn-reginfo-ex-to-register-blocks.md)。

-   WMIREG\_操作\_更新\_GUID 来添加或删除对块的支持，或更改已注册的块的静态实例名称。

    在响应中，WMI 将发送[ **IRP\_MN\_REGINFO** ](https://msdn.microsoft.com/library/windows/hardware/ff551731)或者[ **IRP\_MN\_REGINFO\_EX** ](https://msdn.microsoft.com/library/windows/hardware/ff551734)与该驱动程序请求**Parameters.Wmi.DataPath**设置为 WMIUPDATE。

    驱动程序提供 WMI 使用在其中更新的注册信息：

    -   驱动程序设置 WMIREG\_标志\_删除\_GUID，以便删除对该块的支持。

    -   驱动程序将清除 WMIREG\_标志\_删除\_GUID，以便添加新的块或更新现有块。

    -   该驱动程序设置或清除 WMIREG\_标志\_实例\_*XXX*并提供要更改的块的静态实例名称，或将其更改为使用动态实例的任何必要的实例名称信息名称。

-   WMIREG\_操作\_取消注册，以指示驱动程序将不再提供 WMI 信息的 WMI。

    WMI 不会发送**IRP\_MN\_REGINFO**或**IRP\_MN\_REGINFO\_EX**请求以响应此调用，因为它需要从驱动程序的任何进一步的信息。 驱动程序通常注销响应其块[ **IRP\_MN\_删除\_设备**](https://msdn.microsoft.com/library/windows/hardware/ff551738)请求。 请注意，只有在完成后到设备的所有 WMI Irp 会阻止取消注册调用。 如果驱动程序队列 WMI Irp，它必须取消它们，然后再调[ **IoWMIRegistrationControl** ](https://msdn.microsoft.com/library/windows/hardware/ff550480)能够取消注册。

 

 




