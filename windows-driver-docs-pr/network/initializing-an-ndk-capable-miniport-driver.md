---
title: 初始化支持 NDK 微型端口驱动程序
description: 支持 Network Direct 内核 (NDK) 的微型端口驱动程序初始化其他微型端口驱动程序的方式相同。 但是，它还必须注册其他 NDKPI 入口点。
ms.assetid: 9C9799AB-75A8-4E9A-8702-D389B73522DC
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1650f8766e58d6521eb11d46bb613d58364d951b
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527028"
---
# <a name="initializing-an-ndk-capable-miniport-driver"></a>初始化支持 NDK 微型端口驱动程序


支持 Network Direct 内核 (NDK) 的微型端口驱动程序初始化其他微型端口驱动程序的方式相同。 但是，它还必须注册其他 NDKPI 入口点。

-   [DriverEntry 函数](#driverentry-function)
-   [MiniportSetOptions 函数](#miniportsetoptions-function)
-   [相关的主题](#related-topics)

## <a name="driverentry-function"></a>DriverEntry 函数


每个微型端口驱动程序[ *DriverEntry* ](https://msdn.microsoft.com/library/windows/hardware/ff544113)函数初始化[ **NDIS\_微型端口\_驱动程序\_特征** ](https://msdn.microsoft.com/library/windows/hardware/ff565958)结构，并将其传递给[ **NdisMRegisterMiniportDriver** ](https://msdn.microsoft.com/library/windows/hardware/ff563654)中的以下页面所述：

-   [初始化微型端口驱动程序](initializing-a-miniport-driver.md)
-   [**DriverEntry 的 NDIS 微型端口驱动程序函数**](https://msdn.microsoft.com/library/windows/hardware/ff548818)

支持 NDK 微型端口驱动程序初始化时必须执行以下操作[ **NDIS\_微型端口\_驱动程序\_特征**](https://msdn.microsoft.com/library/windows/hardware/ff565958)结构：

-   在中**OidRequestHandler**成员，微型端口驱动程序必须注册[ *MiniportOidRequest* ](https://msdn.microsoft.com/library/windows/hardware/ff559416)支持的函数：

    -   所有[NDKPI Oid](https://msdn.microsoft.com/library/windows/hardware/jj206455)。

    -   一般情况下是强制性的 NDIS 微型端口驱动程序任何 Oid。

        **请注意**  这些必需的 Oid 的列表，请参阅[微型端口驱动程序的必需 Oid](https://msdn.microsoft.com/library/windows/hardware/ff557139)。

         

-   在中**SetOptionsHandler**成员，微型端口驱动程序必须注册[ *MiniportSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff559443)函数中所述[可选配置微型端口驱动程序服务](configuring-optional-miniport-driver-services.md)以及下面的 MiniportSetOptions 函数部分。

## <a name="miniportsetoptions-function"></a>MiniportSetOptions 函数


NDIS 调用[ *MiniportSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff559443)函数中的微型端口驱动程序之后，立即[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff548818)函数返回。 *MiniportSetOptions*微型端口驱动程序的调用的上下文中调用函数[ **NdisMRegisterMiniportDriver**](https://msdn.microsoft.com/library/windows/hardware/ff563654)。

在其[ *MiniportSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff559443)函数，支持 NDK 微型端口驱动程序注册中所述的以下的所需的 NDKPI 函数入口点及其 NDK 功能和寄存器[配置可选的微型端口驱动程序服务](configuring-optional-miniport-driver-services.md):

-   *OpenNDKAdapterHandler* ([*OPEN\_NDK\_ADAPTER\_HANDLER*](https://msdn.microsoft.com/library/windows/hardware/hh440105))

-   *CloseNDKAdapterHandler* ([*CLOSE\_NDK\_ADAPTER\_HANDLER*](https://msdn.microsoft.com/library/windows/hardware/hh439355))

注册 NDKPI 入口点的这些函数的微型端口驱动程序[ *MiniportSetOptions* ](https://msdn.microsoft.com/library/windows/hardware/ff559443)函数必须执行以下操作：

1.  初始化[ **NDIS\_NDK\_提供程序\_特征**](https://msdn.microsoft.com/library/windows/hardware/hh451566)结构。

    **请注意**  特别注意**标头**成员说明。 微型端口驱动程序必须将此成员设置正确以将自己标识为支持 NDK 微型端口驱动程序。

     

2.  存储在函数入口点**OpenNDKAdapterHandler**并**CloseNDKAdapterHandler**结构的成员。

3.  调用[ **NdisSetOptionalHandlers** ](https://msdn.microsoft.com/library/windows/hardware/ff564550)函数，传递中的结构*OptionalHandlers*参数。

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口 (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






