---
title: 访问操作区域
description: 访问操作区域
ms.assetid: 9a1aa29e-679c-4f7f-a16c-3e1c94be66a7
keywords:
- ACPI 设备 WDK，操作区域
- 操作区域 WDK ACPI
- 功能的驱动程序 WDK ACPI，操作区域
- WDM 函数驱动程序 WDK ACPI，操作区域
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5a8bb43106093c91786fbbb8999fe3fc809d6f5e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56545189"
---
# <a name="accessing-an-operation-region"></a>访问操作区域





当功能驱动程序注册的操作区域处理程序时，该驱动程序必须指定访问类型 ACPI\_OPREGION\_访问权限\_AS\_COOKED。 加工的访问权限支持传输的信息从 ACPI 设备到设备的功能驱动程序，但不能从功能驱动程序到设备。

只有系统提供 ACPI 驱动程序修改操作区域中的数据。 功能驱动程序可以读取操作区域中的数据。 但是，它不能修改数据。 调用时，操作区域处理程序将传输到和从 ACPI 驱动程序的数据缓冲区的操作区域中的字节。 ACPI 驱动程序管理访问正确的字节读取和写入操作的区域中的数据字段。

 

 




