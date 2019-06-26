---
Description: 用户模式驱动程序框架 (UMDF) 要求驱动程序支持插即用 (PnP) 操作的 IPnpCallback 接口和 IPnpCallbackSelfManagedIo 接口的电源管理操作。
title: 支持插即用 (PnP) 和电源管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e13508feaaf868bca8aeb08324511ce4555b3dc5
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387180"
---
# <a name="supporting-plug-and-play-pnp-and-power-management"></a>支持插即用 (PnP) 和电源管理


用户模式驱动程序框架 (UMDF) 要求驱动程序支持[ **IPnpCallback** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallback)插即用 (PnP) 操作的接口和[ **IPnpCallbackSelfManagedIo** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallbackselfmanagedio)电源管理操作的接口。

第一个接口， **IPnpCallback**支持方法调用时插入中的用户或断开，其设备。 第二个接口， **IPnpCallbackSelfManagedIo**支持设备进入低功耗状态，或返回到其工作状态时调用的方法。

除其中一个 WPD 示例模拟硬件，因为这些接口的方法执行任何有意义的工作，并立即返回。

WpdBasicHardwareDriver 示例是一个例外。 此驱动程序支持实际硬件，因为它包含两个方法中的工作代码**IPnpCallback**接口。 支持此示例的两个方法都[ **IPnpCallback::OnD0Entry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallback-ond0entry)并[ **IPnpCallback::OnD0Exit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallback-ond0exit)。 第一种方法检索到的示例驱动程序使用将 I/O 请求转发到内核模式 RS232 驱动程序的 I/O 目标的指针。 检索此指针后**IPnpCallback::OnDOEntry**方法启动 I/O 目标。 第二种方法， **IPnpCallback::OnD0Exit**检索指向 I/O 目标，然后停止它。

如果您的驱动程序支持的硬件，您将想要添加的一个，或这两个接口的支持。 即插即用的完整说明和用户模式设备驱动程序中的电源管理，请参阅[PnP 和电源管理方案，在 UMDF](https://docs.microsoft.com/windows-hardware/drivers/wdf/pnp-and-power-management-scenarios-in-umdf)。

## <a name="span-idrelatedtopicsspanrelated-topics"></a><span id="related_topics"></span>相关主题


[**IPnpCallback**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallback)

[**IPnpCallback::OnD0Entry**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallback-ond0entry)

[**IPnpCallback::OnD0Exit**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nf-wudfddi-ipnpcallback-ond0exit)

[**IPnpCallbackSelfManagedIo**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wudfddi/nn-wudfddi-ipnpcallbackselfmanagedio)

[在 UMDF PnP 和电源管理方案](https://docs.microsoft.com/windows-hardware/drivers/wdf/pnp-and-power-management-scenarios-in-umdf)

 

 





