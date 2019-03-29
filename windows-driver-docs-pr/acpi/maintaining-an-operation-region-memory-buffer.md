---
title: 维护操作区域内存缓冲区
description: 维护操作区域内存缓冲区
ms.assetid: 4abe82ec-d8c4-43c1-a72f-5114ba07160e
keywords:
- ACPI 设备 WDK，操作区域
- 操作区域 WDK ACPI
- 功能的驱动程序 WDK ACPI，操作区域
- WDM 函数驱动程序 WDK ACPI，操作区域
- 操作区域内存缓冲区 WDK ACPI
- 内存缓冲区 WDK ACPI
ms.date: 01/24/2018
ms.localizationpriority: medium
ms.openlocfilehash: 6b8abd68c6a0e1d10f05d3f996348b799da1e3ee
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577196"
---
# <a name="maintaining-an-operation-region-memory-buffer"></a>维护操作区域内存缓冲区



该驱动程序维护的操作区域的内存缓冲区。 内存缓冲区包含与运营区域相关联的数据字段。 ACPI 驱动程序调用的操作区域处理程序，若要访问的操作区域的内存缓冲区中的数据字段。

操作区域内存缓冲区必须符合以下要求：

-   必须从不可分页系统内存分配的内存缓冲区。

-   缓冲区大小必须大于或等于为 ACPI 设备定义的操作区域的大小。

-   缓冲区必须分配之前，驱动程序注册的操作区域处理程序访问它，并维护，只要注册处理程序。

有关操作区域的约束的详细信息，请参阅[高级配置和电源接口规范](https://go.microsoft.com/fwlink/p/?linkid=866846)。

 

 



