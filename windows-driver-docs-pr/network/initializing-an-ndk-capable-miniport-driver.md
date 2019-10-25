---
title: 初始化支持 NDK 的微型端口驱动程序
description: 支持网络直接内核（NDK）的微型端口驱动程序的初始化方式与其他微型端口驱动程序相同。 但是，它还必须注册其他 NDKPI 入口点。
ms.assetid: 9C9799AB-75A8-4E9A-8702-D389B73522DC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6c2d265e369276bf66a50d560e08ab028f5b9627
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824485"
---
# <a name="initializing-an-ndk-capable-miniport-driver"></a>初始化支持 NDK 的微型端口驱动程序


支持网络直接内核（NDK）的微型端口驱动程序的初始化方式与其他微型端口驱动程序相同。 但是，它还必须注册其他 NDKPI 入口点。

-   [DriverEntry 函数](#driverentry-function)
-   [MiniportSetOptions 函数](#miniportsetoptions-function)
-   [相关主题](#related-topics)

## <a name="driverentry-function"></a>DriverEntry 函数


每个微型端口驱动程序的[*DriverEntry*](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize)函数都初始化[**NDIS\_微型\_驱动程序\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)结构，并将其传递给[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver) ，如以下页面所述：

-   [初始化微型端口驱动程序](initializing-a-miniport-driver.md)
-   [**DriverEntry NDIS 微型端口驱动程序函数**](https://docs.microsoft.com/windows-hardware/drivers/network/initializing-a-miniport-driver)

支持 NDK 的微型端口驱动程序必须在初始化[**NDIS\_微型端口\_驱动程序\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_driver_characteristics)结构时执行以下操作：

-   在**OidRequestHandler**成员中，微型端口驱动程序必须注册支持的[*MiniportOidRequest*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_oid_request)函数：

    -   所有[NDKPI oid](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/index)。

    -   通常为 NDIS 微型端口驱动程序所必需的任何 Oid。

        **请注意**  有关这些必需 oid 的列表，请参阅[微型端口驱动程序的必需 oid](https://docs.microsoft.com/windows-hardware/drivers/network/mandatory-oids-for-miniport-drivers)。

         

-   在**SetOptionsHandler**成员中，微型端口驱动程序必须注册[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数，如[配置可选微型端口驱动程序服务](configuring-optional-miniport-driver-services.md)和以下 MiniportSetOptions 函数部分所述。

## <a name="miniportsetoptions-function"></a>MiniportSetOptions 函数


在微型端口驱动程序的[**DriverEntry**](https://docs.microsoft.com/windows-hardware/drivers/network/initializing-a-miniport-driver)函数返回后，NDIS 会立即调用[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数。 在微型端口驱动程序对[**NdisMRegisterMiniportDriver**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismregisterminiportdriver)的调用的上下文中调用*MiniportSetOptions*函数。

在[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数中，支持 ndk 的微型端口驱动程序将注册其 NDK 功能并注册以下必需的 NDKPI 函数入口点，如[配置可选微型端口驱动程序服务](configuring-optional-miniport-driver-services.md)中所述：

-   *OpenNDKAdapterHandler* （[*打开\_NDK\_适配器\_处理程序*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndisndk/nc-ndisndk-open_ndk_adapter_handler)）

-   *CloseNDKAdapterHandler* （[*CLOSE\_NDK\_适配器\_处理程序*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndisndk/nc-ndisndk-close_ndk_adapter_handler)）

若要为这些函数注册 NDKPI 入口点，微型端口驱动程序的[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数必须执行以下操作：

1.  [ **\_特征结构初始化 NDIS\_NDK\_提供程序**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndisndk/ns-ndisndk-_ndis_ndk_provider_characteristics)。

    **请注意**  特别注意**标头**成员说明。 微型端口驱动程序必须正确设置此成员，以将自身标识为支持 NDK 的微型端口驱动程序。

     

2.  将函数入口点存储到结构的**OpenNDKAdapterHandler**和**CloseNDKAdapterHandler**成员中。

3.  调用[**NdisSetOptionalHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)函数，并在*OptionalHandlers*参数中传递结构。

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口（NDKPI）](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






