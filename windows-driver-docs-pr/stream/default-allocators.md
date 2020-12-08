---
title: 默认分配器
description: 默认分配器
keywords:
- 默认分配器 WDK 内核流式处理
- 系统内存分配器 WDK 内核流式处理
- 内存分配器 WDK 内核流式处理
- 多个目标接收器，WDK 内核流式处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a435a720b3ec73bc80705d6985271c7b3da97abe
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817951"
---
# <a name="default-allocators"></a>默认分配器





默认分配器为从系统内存传输数据并需要特定内存分配属性的设备驱动程序提供系统内存分配器。 使用默认分配器时，筛选器只需处理分配器要求请求。

如果使用默认分配器，则微型驱动程序必须 \_ \_ \_ 在相关 [**KSALLOCATOR \_ 组帧**](/windows-hardware/drivers/ddi/ks/ns-ks-ksallocator_framing)结构的 **RequirementsFlags** 成员中设置 KSALLOCATOR REQUIREMENTF 系统内存标志。 \_提交 irp MJ \_ create 并且 create TYPE 为 KSCREATE \_ REQUEST \_ 分配器时，该筛选器通过调用 [**KsCreateDefaultAllocator**](/windows-hardware/drivers/ddi/ks/nf-ks-kscreatedefaultallocator)函数将 IRP 转发到默认分配器处理程序。 所有剩余处理都由默认分配器进行处理。

 

