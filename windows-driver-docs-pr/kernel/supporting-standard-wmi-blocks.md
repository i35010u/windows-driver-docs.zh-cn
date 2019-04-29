---
title: 支持标准 WMI 块
description: 支持标准 WMI 块
ms.assetid: ddec3afb-8274-4eff-93ef-b0a07fd7c13a
keywords:
- WMI WDK 内核，事件块
- 事件阻止 WDK WMI
- 数据将阻止 WDK WMI
- WMI WDK 内核，数据块
- 块 WDK WMI
- 标准块 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: ee18351c104f7d79c262528f9153d066004d663d
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63378002"
---
# <a name="supporting-standard-wmi-blocks"></a>支持标准 WMI 块





每个驱动程序应支持任何*标准块*定义其类型的驱动程序。 标准块向给定的类型，而不考虑供应商的所有设备的 WMI 客户端提供一致的数据。

若要支持的标准块，驱动程序：

-   注册 WMI，以及支持的驱动程序，如中所述的其他标准和自定义块块[注册为 WMI 数据提供程序](registering-as-a-wmi-data-provider.md)。

-   处理指定驱动程序的设备对象指针上的所有 WMI 请求**Parameters.WMI.ProviderId**和处的标准块 GUID **Parameters.WMI.DataPath**中所述，[处理 WMI 请求](handling-wmi-requests.md)。

在系统提供的 MOF 文件中发布的标准块 MOF 类。 驱动程序必须不重新定义其自己的 MOF 文件中的标准块，因为这样做会复制 WMI 数据库中的块。

目前，文件 wmicore.mof，后者包含在 Windows Driver Kit (WDK) 中发布的标准块的类定义。

 

 




