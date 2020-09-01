---
title: 初始化支持 NDK 的微型端口驱动程序
description: 支持网络直接内核 (NDK) 的微型端口驱动程序的初始化方式与其他微型端口驱动程序相同。 但是，它还必须注册其他 NDKPI 入口点。
ms.assetid: 9C9799AB-75A8-4E9A-8702-D389B73522DC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4759dbe7ad151d257550d08f0f8537d2a45fd77
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89207908"
---
# <a name="initializing-an-ndk-capable-miniport-driver"></a>初始化支持 NDK 的微型端口驱动程序


支持网络直接内核 (NDK) 的微型端口驱动程序的初始化方式与其他微型端口驱动程序相同。 但是，它还必须注册其他 NDKPI 入口点。

-   [DriverEntry 函数](#driverentry-function)
-   [MiniportSetOptions 函数](#miniportsetoptions-function)
-   [相关主题](#related-topics)

## <a name="driverentry-function"></a>DriverEntry 函数


每个微型端口驱动程序的 [*DriverEntry*](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 函数都初始化 [**NDIS \_ 微型端口 \_ 驱动程序 \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics) 结构，并将其传递给 [**NdisMRegisterMiniportDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver) ，如以下页面所述：

-   [初始化微型端口驱动程序](initializing-a-miniport-driver.md)
-   [**DriverEntry NDIS 微型端口驱动程序函数**](./initializing-a-miniport-driver.md)

在初始化 [**NDIS \_ 微型端口 \_ 驱动程序 \_ 特征**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics) 结构时，支持 NDK 的微型端口驱动程序必须执行以下操作：

-   在 **OidRequestHandler** 成员中，微型端口驱动程序必须注册支持的 [*MiniportOidRequest*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request) 函数：

    -   所有 [NDKPI oid](/windows-hardware/drivers/ddi/ntddndis/index)。

    -   通常为 NDIS 微型端口驱动程序所必需的任何 Oid。

        **注意**   有关这些必需 Oid 的列表，请参阅[小型端口驱动程序的必需 oid](./mandatory-oids-for-miniport-drivers.md)。

         

-   在 **SetOptionsHandler** 成员中，微型端口驱动程序必须注册 [*MiniportSetOptions*](/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options) 函数，如 [配置可选微型端口驱动程序服务](configuring-optional-miniport-driver-services.md) 和以下 MiniportSetOptions 函数部分所述。

## <a name="miniportsetoptions-function"></a>MiniportSetOptions 函数


在微型端口驱动程序的[**DriverEntry**](./initializing-a-miniport-driver.md)函数返回后，NDIS 会立即调用[*MiniportSetOptions*](/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数。 在微型端口驱动程序对[**NdisMRegisterMiniportDriver**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)的调用的上下文中调用*MiniportSetOptions*函数。

在 [*MiniportSetOptions*](/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options) 函数中，支持 ndk 的微型端口驱动程序将注册其 NDK 功能并注册以下必需的 NDKPI 函数入口点，如 [配置可选微型端口驱动程序服务](configuring-optional-miniport-driver-services.md)中所述：

-   *OpenNDKAdapterHandler* ([*打开 \_ NDK \_ 适配器 \_ 处理程序*](/windows-hardware/drivers/ddi/ndisndk/nc-ndisndk-open_ndk_adapter_handler)) 

-   *CloseNDKAdapterHandler* ([*关闭 \_ NDK \_ 适配器 \_ 处理程序*](/windows-hardware/drivers/ddi/ndisndk/nc-ndisndk-close_ndk_adapter_handler)) 

若要为这些函数注册 NDKPI 入口点，微型端口驱动程序的 [*MiniportSetOptions*](/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options) 函数必须执行以下操作：

1.  初始化 [**NDIS \_ NDK \_ 提供程序 \_ 特征**](/windows-hardware/drivers/ddi/ndisndk/ns-ndisndk-_ndis_ndk_provider_characteristics) 结构。

    **注意**   请特别注意**标头**成员说明。 微型端口驱动程序必须正确设置此成员，以将自身标识为支持 NDK 的微型端口驱动程序。

     

2.  将函数入口点存储到结构的 **OpenNDKAdapterHandler** 和 **CloseNDKAdapterHandler** 成员中。

3.  调用 [**NdisSetOptionalHandlers**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers) 函数，并在 *OptionalHandlers* 参数中传递结构。

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口 (NDKPI)](./overview-of-network-direct-kernel-provider-interface--ndkpi-.md)

 

