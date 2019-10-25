---
title: 注册 WAN 地址系列
description: 注册 WAN 地址系列
ms.assetid: 31443e99-24d8-4276-8345-004b0eeb05d7
keywords:
- CoNDIS WAN 驱动程序 WDK 网络，TAPI 地址系列
- NdisCmRegisterAddressFamilyEx
- TAPI WDK 网络
- 正在注册 WAN address 系列
- WAN 地址系列 WDK 网络
- 地址系列 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 51473ebe69e5fc23e0fda4e3ccac3da5afd58321
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842067"
---
# <a name="registering-the-wan-address-family"></a>注册 WAN 地址系列





本主题介绍如何从 CoNDIS WAN 微型端口调用管理器（MCM）或单独的调用管理器注册 TAPI 地址系列。

两种类型的呼叫管理器都调用[**NdisCmRegisterAddressFamilyEx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndiscmregisteraddressfamilyex)函数来注册其呼叫管理器入口点和地址族类型 CO\_ADDRESS\_系列\_TAPI\_代理。 通过此操作，驱动程序指示它提供 TAPI 服务。 有关在 CoNDIS 驱动程序中注册地址族的详细信息，请参阅[注册和打开地址族](registering-and-opening-an-address-family.md)。

NDIS 通知 NDPROXY 新注册的地址族。 NDPROXY 确定它可以使用呼叫管理器提供的 TAPI 服务。 NDPROXY 打开与驱动程序相关联的 TAPI 代理地址系列，并向 NDIS 注册 NDPROXY 的面向连接的入口点。 这些入口点用于与驱动程序通信。

NDPROXY 可以枚举微型端口驱动程序的 TAPI 功能，并在以后发送在 NDIS 结构中封装的 TAPI 请求。 有关将 CoNDIS 扩展用于 TAPI 支持的详细信息，请参阅[支持 Telephonic 服务的 CONDIS WAN 操作](condis-wan-operations-that-support-telephonic-services.md)。

 

 





