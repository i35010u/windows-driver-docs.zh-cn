---
title: 维护操作区域内存缓冲区
description: 维护操作区域内存缓冲区
keywords:
- ACPI 设备 WDK，操作区域
- 操作区域 WDK ACPI
- 函数驱动程序 WDK ACPI，操作区域
- WDM 函数驱动程序 WDK ACPI，操作区域
- 操作区域内存缓冲区 WDK ACPI
- 内存缓冲区 WDK ACPI
ms.date: 05/19/2020
ms.localizationpriority: medium
ms.openlocfilehash: 7890dfa887b8db27228e0b16a22e952c405d55a6
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785063"
---
# <a name="maintaining-an-operation-region-memory-buffer"></a>维护操作区域内存缓冲区

驱动程序维护一个操作区域内存缓冲区。 内存缓冲区包含与操作区域关联的数据字段。 ACPI 驱动程序调用操作区域处理程序，以访问操作区域内存缓冲区中的数据字段。

操作区域内存缓冲区必须符合以下要求：

- 必须从不可分页系统内存中分配内存缓冲区。

- 缓冲区大小必须大于或等于为 ACPI 设备定义的操作区域的大小。

- 必须先分配缓冲区，驱动程序才会注册访问它的操作区域处理程序，只要注册了处理程序，就会保留该缓冲区。

有关对操作区域的约束的详细信息，请参阅 [高级配置和电源接口规范](https://uefi.org/specifications)。
