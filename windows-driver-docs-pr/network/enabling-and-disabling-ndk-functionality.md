---
title: 启用和禁用 NDK 功能
description: 为启用或禁用 NDK 功能，NDIS 发出 OID_NDK_SET_STATE OID 请求。 支持 NDK 的微型端口驱动程序必须在 MiniportOidRequest 函数中注册此 OID 的支持。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dbb18e546fdcf71533cd95b941faf22d0c0a5651
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822959"
---
# <a name="enabling-and-disabling-ndk-functionality"></a>启用和禁用 NDK 功能


若要启用或禁用 NDK 功能，NDIS [将发出 OID \_ NDK \_ 集 \_ 状态](./oid-ndk-set-state.md) OID 请求。 支持 NDK 的微型端口驱动程序必须在 [*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) 函数中注册此 OID 的支持。

## <a name="determining-whether-ndk-functionality-can-be-enabled"></a>确定是否可以启用 NDK 功能


**\* NetworkDirect** 关键字确定是否可以启用微型端口驱动程序的 NDK 功能。

如果此关键字值设置为 1 ( "Enabled" ) ，则可以启用 NDK 功能。

如果将其设置为 0 ( "Disabled" ) ，则无法启用 NDK 功能。

安装微型端口驱动程序时，默认情况下，其 INF 文件会将此关键字值设置为 1 ( "Enabled" ) 。 有关详细信息，请参阅 [NDKPI 的 INF 要求](inf-requirements-for-ndkpi.md)。

安装微型端口驱动程序后，管理员可以通过在适配器的 "**高级**" 属性页中设置新值来更新 **\* NetworkDirect** 关键字值。 有关高级属性的详细信息，请参阅 [指定高级属性页的配置参数](specifying-configuration-parameters-for-the-advanced-properties-page.md)。

**注意**   在适配器的 " **高级** " 属性页中进行更改后，会自动重新启动微型端口驱动程序。

 

## <a name="when-to-enable-or-disable-ndk-functionality"></a>何时启用或禁用 NDK 功能


此状态更改可由 [OID \_ NDK \_ 集 \_ 状态](./oid-ndk-set-state.md) OID 请求触发，或者在适配器本身中成功或失败时触发。

## <a name="enabling-or-disabling-ndk-functionality"></a>启用或禁用 NDK 功能


若要启用或禁用其 NDK 功能，微型端口驱动程序必须将 **NetEventNDKEnable** 或 **NetEventNDKDisable** 即插即用 (PnP) 事件发送到 NDIS。

若要发送 PnP 事件，微型端口驱动程序将 [**调用 NdisMNetPnPEvent**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent)函数，并设置 *NetPnPEvent* 参数指向的 [**NET \_ PnP \_ 事件 \_ 通知**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event_notification)结构的 **NetPnPEvent** 成员，如下所示：

-   **NetEventNDKEnable** 如果要启用 NDK 功能，则为。

-   **NetEventNDKDisable** 如果要禁用 NDK 功能，则为。

**NetEventNDKDisable** PnP 事件触发 NDIS 和上层驱动程序，以便在正在禁用 ndk 功能的适配器上，开始关闭其打开的 [**NDK \_ 适配器**](/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_adapter)实例。 PnP 事件将保持挂起状态，直到适配器上所有打开的 **NDK \_ 适配器** 实例关闭。

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口 (NDKPI)](./overview-of-network-direct-kernel-provider-interface--ndkpi-.md)

 

