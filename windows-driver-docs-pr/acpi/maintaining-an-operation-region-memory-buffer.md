---
title: 维护操作区域内存缓冲区
description: 维护操作区域内存缓冲区
ms.assetid: 4abe82ec-d8c4-43c1-a72f-5114ba07160e
keywords:
- ACPI 设备 WDK，操作区域
- 操作区域 WDK ACPI
- 函数驱动程序 WDK ACPI，操作区域
- WDM 函数驱动程序 WDK ACPI，操作区域
- 操作区域内存缓冲区 WDK ACPI
- 内存缓冲区 WDK ACPI
ms.date: 05/19/2020
ms.localizationpriority: medium
ms.openlocfilehash: 79ce8e07cc5a005a798e87d08db3d8dfb812d039
ms.sourcegitcommit: cbcb712a9f1f62c7d67e1b98097a0d8d24bd0c71
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/21/2020
ms.locfileid: "83769335"
---
# <a name="maintaining-an-operation-region-memory-buffer"></a>维护操作区域内存缓冲区

驱动程序维护一个操作区域内存缓冲区。 内存缓冲区包含与操作区域关联的数据字段。 ACPI 驱动程序调用操作区域处理程序，以访问操作区域内存缓冲区中的数据字段。

操作区域内存缓冲区必须符合以下要求：

- 必须从不可分页系统内存中分配内存缓冲区。

- 缓冲区大小必须大于或等于为 ACPI 设备定义的操作区域的大小。

- 必须先分配缓冲区，驱动程序才会注册访问它的操作区域处理程序，只要注册了处理程序，就会保留该缓冲区。

有关对操作区域的约束的详细信息，请参阅[高级配置和电源接口规范](https://uefi.org/specifications)。
