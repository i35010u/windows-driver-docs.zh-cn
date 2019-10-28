---
title: 启用和禁用 NDK 功能
description: 若要启用或禁用 NDK 功能，NDIS 会发出 OID_NDK_SET_STATE OID 请求。 支持 NDK 的微型端口驱动程序必须在 MiniportOidRequest 函数中注册此 OID 的支持。
ms.assetid: A72AD98E-FF84-48FF-B627-5534231244B0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db6915b5d8aa8d3fc41db792b3e2e1277d94d2b0
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838124"
---
# <a name="enabling-and-disabling-ndk-functionality"></a>启用和禁用 NDK 功能


若要启用或禁用 NDK 功能，NDIS [\_NDK\_集\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-ndk-set-state)OID 请求发出 OID。 支持 NDK 的微型端口驱动程序必须在[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)函数中注册此 OID 的支持。

## <a name="determining-whether-ndk-functionality-can-be-enabled"></a>确定是否可以启用 NDK 功能


**\*NetworkDirect**关键字确定是否可以启用微型端口驱动程序的 NDK 功能。

如果此关键字值设置为1（"Enabled"），则可以启用 NDK 功能。

如果设置为0（"Disabled"），则无法启用 NDK 功能。

安装微型端口驱动程序时，默认情况下，其 INF 文件会将此关键字值设置为1（"Enabled"）。 有关详细信息，请参阅[NDKPI 的 INF 要求](inf-requirements-for-ndkpi.md)。

安装微型端口驱动程序后，管理员可以通过在适配器的 "**高级**" 属性页中设置新值来更新 **\*NetworkDirect**关键字值。 有关高级属性的详细信息，请参阅[指定高级属性页的配置参数](specifying-configuration-parameters-for-the-advanced-properties-page.md)。

**请注意**   在适配器的 "**高级**" 属性页中进行更改后，会自动重新启动微型端口驱动程序。

 

## <a name="when-to-enable-or-disable-ndk-functionality"></a>何时启用或禁用 NDK 功能


此状态更改可由[OID\_NDK\_设置\_状态](https://docs.microsoft.com/windows-hardware/drivers/network/oid-ndk-set-state)OID 请求，或者适配器本身中的成功或失败触发。

## <a name="enabling-or-disabling-ndk-functionality"></a>启用或禁用 NDK 功能


若要启用或禁用其 NDK 功能，微型端口驱动程序必须将**NetEventNDKEnable**或**NetEventNDKDisable**即插即用（PnP）事件发送到 NDIS。

若要发送 PnP 事件，微型端口驱动程序将调用[**NdisMNetPnPEvent**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismnetpnpevent)函数，并设置[**NET\_PnP\_事件**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_net_pnp_event_notification)的**NetPnPEvent**成员\_通知结构， *NetPnPEvent*参数指向，如下所示：

-   **NetEventNDKEnable**如果要启用 NDK 功能，则为。

-   **NetEventNDKDisable**如果要禁用 NDK 功能，则为。

**NetEventNDKDisable** PnP 事件触发 NDIS 和上层驱动程序，以便在正在禁用 NDK 功能的适配器上，开始关闭其打开的[**NDK\_适配器**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndkpi/ns-ndkpi-_ndk_adapter)实例。 PnP 事件将保持挂起状态，直到所有打开的**NDK\_** 适配器上的所有打开的 NDK 适配器实例关闭。

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口（NDKPI）](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






