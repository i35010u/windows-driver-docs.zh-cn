---
title: 将总线相对地址映射到虚拟地址
description: 将总线相对地址映射到虚拟地址
keywords:
- 虚拟地址空间映射 WDK 内核
- 物理地址空间映射 WDK 内核
- 映射内存
- 地址空间映射 WDK 内核
- 转换地址空间 WDK 内核
- 内存管理 WDK 内核，映射地址
- 总线相对内存空间 WDK 内核
ms.date: 06/16/2017
ms.localizationpriority: medium
ms.openlocfilehash: 80e686f78cbb041905cdeef110437a23cab1aaae
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96823977"
---
# <a name="mapping-bus-relative-addresses-to-virtual-addresses"></a>将总线相对地址映射到虚拟地址





某些处理器实现单独的内存和 i/o 地址空间，而其他处理器则不实现。 由于硬件平台之间的差异，用来访问 i/o 或内存驻留设备资源的机制与平台不同。

驱动程序请求设备 i/o 和内存资源，以响应 PnP 管理器的 [**IRP \_ MN \_ 查询 \_ 资源 \_ 要求**](./irp-mn-query-resource-requirements.md) IRP。 根据硬件体系结构，HAL 可以分配 i/o 空间或内存空间中的 i/o 资源，并可以分配 i/o 空间或内存空间中的内存资源。

如果 HAL 使用总线相关的内存空间来访问设备资源 (例如设备寄存器) ，则驱动程序必须将 i/o 空间映射到虚拟内存，以便能够访问这些资源。 驱动程序可以通过在设备启动时通过 PnP 管理器检查由 PnP 管理器传递给驱动程序的已转换资源，来确定资源是否为 i/o 或内存驻留。 如果 HAL 使用 i/o 空间，则不需要映射。

具体而言，当驱动程序收到 [**IRP \_ MN \_ 开始 \_ 设备**](./irp-mn-start-device.md) 请求时，它应检查 **IrpSp- &gt; StartDevice. AllocatedResources** 和 IrpSp StartDevice 之间的 **&gt; 结构**，该结构分别描述了 PnP 管理器分配给设备的原始 (总线相关) 和已转换的资源。 驱动程序应将每个资源列表的副本作为辅助调试保存在设备扩展中。

资源列表是成对的 [**CM \_ 资源 \_ 列表**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_cm_resource_list) 结构，其中原始列表的每个元素对应于已翻译列表的同一个元素。 例如，如果 **AllocatedResources** \[ 0 \] 描述了原始 I/o 端口范围， **AllocatedResourcesTranslated** \[ 0 \] 说明了转换后的相同范围。 每个翻译的资源都包含物理地址和资源的类型。

如果 (**CmResourceTypeMemory**) 为驱动程序分配了已转换的内存资源，则它必须调用 [**MmMapIoSpace**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmmapiospace) 将物理地址映射到可通过其访问设备寄存器的虚拟地址。 若要使驱动程序以独立于平台的方式运行，应检查每个返回的已转换资源，并根据需要对其进行映射。

**内核模式驱动程序应采取以下步骤来响应 IRP \_ MN \_ 启动 \_ 设备请求，以确保对所有设备资源的访问权限**

1.  将 **IrpSp- &gt; StartDevice. AllocatedResources** 复制到设备扩展。

2.  将 **IrpSp- &gt; StartDevice. AllocatedResourcesTranslated** 复制到设备扩展。

3.  在循环中，检查 **AllocatedResourcesTranslated** 中的每个描述符元素。 如果描述符资源类型为 **CmResourceTypeMemory**，则调用 **MmMapIoSpace**，同时传递已转换资源的物理地址和长度。

当驱动程序收到 [**irp \_ MN \_ 停止 \_ 设备**](./irp-mn-stop-device.md) 或 irp MN 从 PnP 管理器 [**\_ \_ 删除 \_ 设备**](./irp-mn-remove-device.md) 请求时，它必须通过在类似循环中调用 [**MmUnmapIoSpace**](/windows-hardware/drivers/ddi/wdm/nf-wdm-mmunmapiospace) 来释放映射。 如果该驱动程序必须失败 **IRP \_ MN \_ 启动 \_ 设备** 请求，则该驱动程序还应调用 **MmUnmapIoSpace** 。

原始资源类型指示驱动程序应调用哪个 HAL 访问例程 (**读取 \_ register \_ _xxx_**，**编写 \_ 寄存器 \_ _xxx_**，**读取 \_ 端口 \_ _xxx_**，**写入 \_ 端口 \_ _xxx_**) 。 大多数驱动程序不必检查原始资源列表来确定要使用的例程，因为驱动程序本身请求资源或驱动程序编写器在给定设备硬件性质的情况下知道所需的类型。

 对于 i/o 空间中的资源 (**CmResourceTypePort**， **CmResourceTypeInterrupt**， **CmResourceTypeDma**) ，驱动程序应使用返回的物理地址的低序位32位来访问设备资源，例如，通过 HAL 的读取和写入 **读取 \_ REGISTER \_ _XXX_**，**写入 \_ REGISTER \_ _xxx_**，**读取 \_ 端口 \_ _xxx_**，**写入 \_ 端口 \_ _xxx_** 例程。
 
 

