---
title: 支持标准 WMI 块
description: 支持标准 WMI 块
keywords:
- WMI WDK 内核，事件块
- 事件块 WDK WMI
- 数据块 WDK WMI
- WMI WDK 内核，数据块
- 阻止 WDK WMI
- 标准块 WDK WMI
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 32587faff1295e3495a22472f3e8ea5de2c477a6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96816625"
---
# <a name="supporting-standard-wmi-blocks"></a>支持标准 WMI 块





每个驱动程序都应支持为其类型的驱动程序定义的任何 *标准块* 。 标准块为 WMI 客户端提供了给定类型的所有设备的一致数据，而不考虑供应商。

若要支持标准块，请执行以下操作：

-   向 WMI 注册块，以及驱动程序支持的其他标准和自定义块，如 [注册为 WMI 数据提供程序](registering-as-a-wmi-data-provider.md)中所述。

-   处理所有 WMI 请求，这些请求在 **参数.** 数据路径中指定驱动程序的设备对象指针，并处理 **参数. wmi**[中的](handling-wmi-requests.md)标准块的 GUID。

标准块的 MOF 类在系统提供的 MOF 文件中发布。 驱动程序不得在其自己的 MOF 文件中重新定义标准块，因为这样做会在 WMI 数据库中重复该程序块。

目前，标准块的类定义发布在文件 wmicore 中，该文件包含在 Windows 驱动程序工具包 (WDK) 中。

 

 




