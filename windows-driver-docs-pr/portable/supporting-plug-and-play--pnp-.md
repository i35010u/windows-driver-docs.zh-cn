---
description: 用户模式驱动程序框架 (UMDF) 需要驱动程序支持用于即插即用 (PnP) 操作的 IPnpCallback 接口和用于电源管理操作的 IPnpCallbackSelfManagedIo 接口。
title: 支持插即用 (PnP) 和电源管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bbf9dd86d6758f4cec6ebb6d9cb0efb3aa494bbd
ms.sourcegitcommit: faff37814159ad224080205ad314cabf412e269f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2020
ms.locfileid: "89384965"
---
# <a name="supporting-plug-and-play-pnp-and-power-management"></a>支持插即用 (PnP) 和电源管理


用户模式驱动程序框架 (UMDF) 需要驱动程序支持用于即插即用 (PnP) 操作的 [**IPnpCallback**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallback) 接口和用于电源管理操作的 [**IPnpCallbackSelfManagedIo**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackselfmanagedio) 接口。

第一个接口（ **IPnpCallback** ）支持用户插入或断开设备时调用的方法。 第二个接口（ **IPnpCallbackSelfManagedIo** ）支持设备进入低功耗状态时调用的方法，或返回到工作状态。

由于 WPD 的所有示例都不会模拟硬件，因此这些接口的方法不执行任何有意义的工作并立即返回。

一个例外是 WpdBasicHardwareDriver 示例。 由于此驱动程序支持实际硬件，因此它包含 **IPnpCallback** 接口中两种方法的工作代码。 此示例支持的两种方法是 [**IPnpCallback：： OnD0Entry**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0entry) 和 [**IPnpCallback：： OnD0Exit**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0exit)。 第一种方法检索指向 i/o 目标的指针，示例驱动程序使用该指针将 i/o 请求转发到内核模式 RS232 驱动程序。 检索此指针后， **IPnpCallback：： OnDOEntry** 方法会启动 i/o 目标。 第二种方法 **IPnpCallback：： OnD0Exit** 检索指向 i/o 目标的指针，然后将其停止。

如果你的驱动程序支持硬件，你将需要为这些接口中的一个或两个提供支持。 有关用户模式设备驱动程序中 PnP 和电源管理的完整说明，请参阅 [UMDF 中的 pnp 和电源管理方案](../wdf/pnp-and-power-management-scenarios-in-umdf.md)。

## <a name="span-idrelated_topicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**IPnpCallback**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallback)

[**IPnpCallback::OnD0Entry**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0entry)

[**IPnpCallback::OnD0Exit**](/windows-hardware/drivers/ddi/wudfddi/nf-wudfddi-ipnpcallback-ond0exit)

[**IPnpCallbackSelfManagedIo**](/windows-hardware/drivers/ddi/wudfddi/nn-wudfddi-ipnpcallbackselfmanagedio)

[UMDF 中的 PnP 和电源管理方案](../wdf/pnp-and-power-management-scenarios-in-umdf.md)

 

