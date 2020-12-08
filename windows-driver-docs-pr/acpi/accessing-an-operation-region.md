---
title: 访问操作区域
description: 访问操作区域
keywords:
- ACPI 设备 WDK，操作区域
- 操作区域 WDK ACPI
- 函数驱动程序 WDK ACPI，操作区域
- WDM 函数驱动程序 WDK ACPI，操作区域
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4119626d70d20b4897cb34fdc2fe0b994ccab3bf
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788001"
---
# <a name="accessing-an-operation-region"></a>访问操作区域





当函数驱动程序注册操作区域处理程序时，驱动程序必须将访问类型 ACPI \_ OPREGION \_ access 指定 \_ 为 \_ 加工。 加工访问支持将信息从 ACPI 设备传输到设备的功能驱动程序，而不支持从函数驱动程序传输到设备。

只有系统提供的 ACPI 驱动程序会修改操作区域中的数据。 函数驱动程序可以读取操作区域中的数据。 但是，它不能修改数据。 调用时，操作区域处理程序会将操作区域中的字节传输到 ACPI 驱动程序的数据缓冲区。 ACPI 驱动程序管理访问正确的字节以读取和写入操作区域中的数据字段。

 

 




