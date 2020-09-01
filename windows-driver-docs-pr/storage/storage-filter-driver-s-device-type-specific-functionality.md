---
title: 存储筛选器驱动程序的特定于设备类型的功能
description: 存储筛选器驱动程序的特定于设备类型的功能
ms.assetid: ecc0d938-e931-46bd-a1e1-0e6da8e149a4
keywords:
- 存储筛选器驱动程序 WDK，特定于设备类型的功能
- 筛选器驱动程序 WDK 存储，特定于设备类型的功能
- SFD WDK 存储，特定于设备类型的功能
- 设备类型特定的功能 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4bc7d4391865c83a03393b6234224deea73d7b80
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89187501"
---
# <a name="storage-filter-drivers-device-type-specific-functionality"></a>存储筛选器驱动程序的特定于设备类型的功能

根据其设备的性质， (SFD) 的存储筛选器驱动程序可能负责以下特定于设备类型的功能：

- 如果设备以非标准格式处理数据，则在发送传输请求之前或之后将数据转换为特定于设备的格式

- 使用 SRBs 为端口驱动程序提供支持的 i/o 控制请求、驱动程序定义的 i/o 控制请求或传递请求（根据其设备的需要）设置 Irp，并将这些 Irp 发送到下一个较低版本的驱动程序

- 根据需要为其设备修改类驱动程序提供的 SRBs

- 为请求建立超时值

- 提供一个或多个 [*IoCompletion*](/windows-hardware/drivers/ddi/wdm/nc-wdm-io_completion_routine) 例程，如相应的存储类驱动程序，为需要特殊处理的特定于设备的请求处理某些错误条件和重试

通常，对于需要特定于设备的处理的请求，SFD 具有与存储类驱动程序相同的职责。 有关存储类驱动程序所需的功能的讨论，请参阅 [存储类驱动程序](introduction-to-storage-class-drivers.md)。