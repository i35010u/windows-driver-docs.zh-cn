---
title: CoNDIS 微型端口驱动程序注册
description: CoNDIS 微型端口驱动程序注册
ms.assetid: 2dfd3bdc-b7b1-4491-b05e-2e8e1f5895b8
keywords:
- 微型端口驱动程序 WDK 网络，CoNDIS
- NDIS 微型端口驱动程序 WDK，CoNDIS
- 注册微型端口驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63dbee2037390337c9beb4cb9ecd6735206e7118
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72838191"
---
# <a name="condis-miniport-driver-registration"></a>CoNDIS 微型端口驱动程序注册





CoNDIS 微型端口驱动程序像其他微型端口驱动程序一样初始化，还必须注册其他 CoNDIS 入口点。 有关微型端口驱动程序初始化的一般信息，请参阅[初始化微型端口驱动程序](initializing-a-miniport-driver.md)。

若要注册*MiniportXxx*函数的 CoNDIS 入口点，CoNDIS 微型端口驱动程序从[*MiniportSetOptions*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-set_options)函数调用[**NdisSetOptionalHandlers**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndissetoptionalhandlers)函数。 在*MiniportSetOptions*中，微型端口驱动程序[**初始化 NDIS\_微型\_联\_特征**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_co_characteristics)结构，并将其传递到**NdisSetOptionalHandlers**的*OptionalHandlers*参数。

微型端口呼叫管理器（MCMs）还在*MiniportSetOptions*中注册*ProtocolXxx*函数。 有关 MCM 驱动程序注册的详细信息，请参阅[CONDIS MCM registration](condis-mcm-registration.md)。

有关配置可选微型端口驱动程序服务的详细信息，请参阅[配置可选微型端口驱动程序服务](configuring-optional-miniport-driver-services.md)。

 

 





