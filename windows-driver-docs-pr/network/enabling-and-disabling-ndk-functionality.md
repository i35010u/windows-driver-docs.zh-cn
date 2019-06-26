---
title: 启用和禁用 NDK 功能
description: 若要启用或禁用 NDK 功能，NDIS 发出 OID_NDK_SET_STATE OID 请求。 NDK 支持的微型端口驱动程序必须在其 MiniportOidRequest 函数中注册此 OID 的支持。
ms.assetid: A72AD98E-FF84-48FF-B627-5534231244B0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 56d1da6f3753cd4770e69bdc1567ff13350f7a49
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67378688"
---
# <a name="enabling-and-disabling-ndk-functionality"></a>启用和禁用 NDK 功能


若要启用或禁用 NDK 功能，NDIS 问题[OID\_NDK\_设置\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-ndk-set-state)OID 请求。 NDK 支持的微型端口驱动程序必须注册支持，使此 OID 中其[ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)函数。

## <a name="determining-whether-ndk-functionality-can-be-enabled"></a>确定是否可以启用 NDK 功能


**\*NetworkDirect**关键字确定是否可以启用 NDK 微型端口驱动程序的功能。

如果该关键字的值设置为 1 （"已启用"），可以启用 NDK 功能。

如果设置为 0 ("Disabled")，则不能启用 NDK 功能。

安装微型端口驱动程序时，其 INF 文件设置为 1 （"已启用"） 具有默认情况下该关键字的值。 有关详细信息，请参阅[NDKPI INF 要求](inf-requirements-for-ndkpi.md)。

安装微型端口驱动程序后，管理员可以更新 **\*NetworkDirect**中设置新值的关键字值**高级**适配器属性页。 有关高级属性的详细信息，请参阅[的高级属性页指定配置参数](specifying-configuration-parameters-for-the-advanced-properties-page.md)。

**请注意**   中进行更改后的微型端口驱动程序将自动重启**高级**适配器属性页。

 

## <a name="when-to-enable-or-disable-ndk-functionality"></a>何时启用或禁用 NDK 功能


此状态更改可由触发[OID\_NDK\_设置\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-ndk-set-state)OID 请求或成功或失败适配器本身。

## <a name="enabling-or-disabling-ndk-functionality"></a>启用或禁用 NDK 功能


若要启用或禁用其 NDK 功能，微型端口驱动程序必须发送**NetEventNDKEnable**或**NetEventNDKDisable**到 NDIS 插即用 (PnP) 事件。

若要发送即插即用事件，微型端口驱动程序调用[ **NdisMNetPnPEvent** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismnetpnpevent)函数，设置**NetPnPEvent**隶属[ **NET\_PNP\_事件\_通知**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_net_pnp_event_notification)结构*NetPnPEvent*参数，如下所示指向：

-   **NetEventNDKEnable**如果 NDK 功能才可用。

-   **NetEventNDKDisable**如果 NDK 功能将被禁用。

**NetEventNDKDisable**即插即用事件触发 NDIS 和上层驱动程序以启动关闭其打开[ **NDK\_适配器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndkpi/ns-ndkpi-_ndk_adapter)通过适配器的实例其中的 NDK 功能被禁用。 即插即用事件将保持挂起状态直至将所有打开的**NDK\_适配器**通过适配器的实例闭合。

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口 (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






