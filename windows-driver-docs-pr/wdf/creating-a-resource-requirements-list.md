---
title: 创建资源要求列表
description: 创建资源要求列表
keywords:
- 硬件资源 WDK KMDF，创建资源需求列表
- 资源要求列出了 WDK KMDF
- 资源要求列出了 WDK KMDF、创建
- 资源需求-列表对象 WDK KMDF
- 框架资源需求-列表对象 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8c34934ceda273ac14f07015100ab01833397899
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829041"
---
# <a name="creating-a-resource-requirements-list"></a>创建资源要求列表


当总线驱动程序检测到子设备时，该驱动程序负责为设备创建资源需求列表。 列表中的每个项都是设备的 [逻辑配置](../kernel/hardware-resources.md#ddk-logical-configurations-kg) 。

当驱动程序在总线枚举过程中报告设备后，框架将调用驱动程序的 [*EvtDeviceResourceRequirementsQuery*](/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resource_requirements_query) 回调函数。 此回调函数接收资源需求列表对象的句柄，该对象表示空资源需求列表。

然后，该驱动程序必须执行以下操作，以将信息添加到资源要求列表：

-   创建一个空的逻辑配置。

    对于驱动程序将指定的每个逻辑配置，驱动程序必须调用 [**WdfIoResourceListCreate**](/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfioresourcelistcreate) 来创建一个空的逻辑配置。

-   将资源描述符添加到逻辑配置。

    若要将资源描述符添加到逻辑配置，驱动程序必须为设备需要的每种类型的硬件资源执行以下操作：

    1.  填写驱动程序分配的 [**IO \_ 资源 \_ 描述符**](/windows-hardware/drivers/ddi/wdm/ns-wdm-_io_resource_descriptor) 结构，此结构指定特定资源的有效值范围。
    2.  调用 [**WdfIoResourceListAppendDescriptor**](/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfioresourcelistappenddescriptor) 或 [**WdfIoResourceListInsertDescriptor**](/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfioresourcelistinsertdescriptor) 将 IO \_ 资源描述符结构的内容添加 \_ 到逻辑配置。

    如果设备使用一个资源类型的多个实例，堆栈中访问该资源的所有驱动程序都必须知道资源的添加顺序。 例如，如果设备需要两个范围的 i/o 端口地址，则访问资源描述符的所有驱动程序必须了解将两个范围添加到逻辑配置的顺序。

-   将逻辑配置添加到资源需求列表。

    若要将逻辑配置添加到设备的资源需求列表，驱动程序将调用 [**WdfIoResourceRequirementsListAppendIoResList**](/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfioresourcerequirementslistappendioreslist) 或 [**WdfIoResourceRequirementsListInsertIoResList**](/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfioresourcerequirementslistinsertioreslist)。

    向设备分配资源时，PnP 管理器会尝试匹配列表中第一个逻辑配置的要求。 如果该配置所需的资源不可用，则 PnP 管理器将与列表中的下一个配置匹配，其中资源可用。

    如果驱动程序支持非 PnP 设备，则驱动程序通常还必须调用 [**WdfIoResourceRequirementsListSetSlotNumber**](/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfioresourcerequirementslistsetslotnumber) 和 [**WdfIoResourceRequirementsListSetInterfaceType**](/windows-hardware/drivers/ddi/wdfresource/nf-wdfresource-wdfioresourcerequirementslistsetinterfacetype)。

驱动程序的 [*EvtDeviceResourceRequirementsQuery*](/windows-hardware/drivers/ddi/wdfpdo/nc-wdfpdo-evt_wdf_device_resource_requirements_query) 回调函数返回后，框架会将资源需求列表传递到 PnP 管理器。

 

