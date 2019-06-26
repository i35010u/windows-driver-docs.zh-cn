---
title: 初始化支持 NDK 的微型端口驱动程序
description: 支持 Network Direct 内核 (NDK) 的微型端口驱动程序初始化其他微型端口驱动程序的方式相同。 但是，它还必须注册其他 NDKPI 入口点。
ms.assetid: 9C9799AB-75A8-4E9A-8702-D389B73522DC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a28600f6afabb6831224844423262b71baa6c098
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381291"
---
# <a name="initializing-an-ndk-capable-miniport-driver"></a>初始化支持 NDK 的微型端口驱动程序


支持 Network Direct 内核 (NDK) 的微型端口驱动程序初始化其他微型端口驱动程序的方式相同。 但是，它还必须注册其他 NDKPI 入口点。

-   [DriverEntry 函数](#driverentry-function)
-   [MiniportSetOptions 函数](#miniportsetoptions-function)
-   [相关主题](#related-topics)

## <a name="driverentry-function"></a>DriverEntry 函数


每个微型端口驱动程序[ *DriverEntry* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)函数初始化[ **NDIS\_微型端口\_驱动程序\_特征** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_driver_characteristics)结构，并将其传递给[ **NdisMRegisterMiniportDriver** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)中的以下页面所述：

-   [初始化微型端口驱动程序](initializing-a-miniport-driver.md)
-   [**DriverEntry 的 NDIS 微型端口驱动程序函数**](https://docs.microsoft.com/windows-hardware/drivers/network/initializing-a-miniport-driver)

支持 NDK 微型端口驱动程序初始化时必须执行以下操作[ **NDIS\_微型端口\_驱动程序\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_driver_characteristics)结构：

-   在中**OidRequestHandler**成员，微型端口驱动程序必须注册[ *MiniportOidRequest* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_oid_request)支持的函数：

    -   所有[NDKPI Oid](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/index)。

    -   一般情况下是强制性的 NDIS 微型端口驱动程序任何 Oid。

        **请注意**  这些必需的 Oid 的列表，请参阅[微型端口驱动程序的必需 Oid](https://docs.microsoft.com/windows-hardware/drivers/network/mandatory-oids-for-miniport-drivers)。

         

-   在中**SetOptionsHandler**成员，微型端口驱动程序必须注册[ *MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)函数中所述[可选配置微型端口驱动程序服务](configuring-optional-miniport-driver-services.md)以及下面的 MiniportSetOptions 函数部分。

## <a name="miniportsetoptions-function"></a>MiniportSetOptions 函数


NDIS 调用[ *MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)函数中的微型端口驱动程序之后，立即[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/network/initializing-a-miniport-driver)函数返回。 *MiniportSetOptions*微型端口驱动程序的调用的上下文中调用函数[ **NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismregisterminiportdriver)。

在其[ *MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)函数，支持 NDK 微型端口驱动程序注册中所述的以下的所需的 NDKPI 函数入口点及其 NDK 功能和寄存器[配置可选的微型端口驱动程序服务](configuring-optional-miniport-driver-services.md):

-   *OpenNDKAdapterHandler* ([*OPEN\_NDK\_ADAPTER\_HANDLER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndisndk/nc-ndisndk-open_ndk_adapter_handler))

-   *CloseNDKAdapterHandler* ([*CLOSE\_NDK\_ADAPTER\_HANDLER*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndisndk/nc-ndisndk-close_ndk_adapter_handler))

注册 NDKPI 入口点的这些函数的微型端口驱动程序[ *MiniportSetOptions* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-set_options)函数必须执行以下操作：

1.  初始化[ **NDIS\_NDK\_提供程序\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndisndk/ns-ndisndk-_ndis_ndk_provider_characteristics)结构。

    **请注意**  特别注意**标头**成员说明。 微型端口驱动程序必须将此成员设置正确以将自己标识为支持 NDK 微型端口驱动程序。

     

2.  存储在函数入口点**OpenNDKAdapterHandler**并**CloseNDKAdapterHandler**结构的成员。

3.  调用[ **NdisSetOptionalHandlers** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndissetoptionalhandlers)函数，传递中的结构*OptionalHandlers*参数。

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口 (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






