---
description: 用户模式驱动程序框架 (UMDF) 需要驱动程序支持用于即插即用 (PnP) 操作的 IPnpCallback 接口和用于电源管理操作的 IPnpCallbackSelfManagedIo 接口。
title: 支持插即用 (PnP) 和电源管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 715c06d0097e5ad7c8211b6af77a8900230dbce8
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969258"
---
# <a name="supporting-plug-and-play-pnp-and-power-management"></a>支持插即用 (PnP) 和电源管理


用户模式驱动程序框架 (UMDF) 需要驱动程序支持用于即插即用 (PnP) 操作的 [**IPnpCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallback) 接口和用于电源管理操作的 [**IPnpCallbackSelfManagedIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackselfmanagedio) 接口。

第一个接口（ **IPnpCallback** ）支持用户插入或断开设备时调用的方法。 第二个接口（ **IPnpCallbackSelfManagedIo** ）支持设备进入低功耗状态时调用的方法，或返回到工作状态。

由于 WPD 的所有示例都不会模拟硬件，因此这些接口的方法不执行任何有意义的工作并立即返回。

一个例外是 WpdBasicHardwareDriver 示例。 由于此驱动程序支持实际硬件，因此它包含 **IPnpCallback** 接口中两种方法的工作代码。 此示例支持的两种方法是 [**IPnpCallback：： OnD0Entry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0entry) 和 [**IPnpCallback：： OnD0Exit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0exit)。 第一种方法检索指向 i/o 目标的指针，示例驱动程序使用该指针将 i/o 请求转发到内核模式 RS232 驱动程序。 检索此指针后， **IPnpCallback：： OnDOEntry** 方法会启动 i/o 目标。 第二种方法 **IPnpCallback：： OnD0Exit** 检索指向 i/o 目标的指针，然后将其停止。

如果你的驱动程序支持硬件，你将需要为这些接口中的一个或两个提供支持。 有关用户模式设备驱动程序中 PnP 和电源管理的完整说明，请参阅 [UMDF 中的 pnp 和电源管理方案](https://docs.microsoft.com/windows-hardware/drivers/wdf/pnp-and-power-management-scenarios-in-umdf)。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**IPnpCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallback)

[**IPnpCallback::OnD0Entry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0entry)

[**IPnpCallback::OnD0Exit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0exit)

[**IPnpCallbackSelfManagedIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackselfmanagedio)

[UMDF 中的 PnP 和电源管理方案](https://docs.microsoft.com/windows-hardware/drivers/wdf/pnp-and-power-management-scenarios-in-umdf)

 

 





