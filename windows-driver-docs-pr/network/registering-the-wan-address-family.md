---
title: 注册 WAN 地址系列
description: 注册 WAN 地址系列
ms.assetid: 31443e99-24d8-4276-8345-004b0eeb05d7
keywords:
- WAN 的 CoNDIS 驱动程序 WDK 网络，TAPI 地址系列
- NdisCmRegisterAddressFamilyEx
- TAPI WDK 网络
- 注册 WAN 地址系列
- WAN 地址系列 WDK 网络
- 地址系列 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c7b0219f1059fb927beb5bda8e91f8683f034e3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67359146"
---
# <a name="registering-the-wan-address-family"></a>注册 WAN 地址系列





本主题介绍如何注册从 CoNDIS WAN 小型端口呼叫管理器 (MCM) 或单独调用管理器的 TAPI 地址族。

调用管理器调用的任何一种[ **NdisCmRegisterAddressFamilyEx** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndiscmregisteraddressfamilyex)函数来注册其调用管理器入口点和地址系列类型共同\_地址\_系列\_TAPI\_代理。 通过此操作，该驱动程序指示它提供 TAPI 服务。 有关注册的 CoNDIS 驱动程序中的地址族的详细信息，请参阅[注册和打开地址族](registering-and-opening-an-address-family.md)。

NDIS 通知 NDPROXY 新注册的地址族。 NDPROXY 确定它可以使用呼叫管理器提供的 TAPI 服务。 NDPROXY 打开与该驱动程序相关联并将注册 NDIS NDPROXY 的面向连接的入口点的 TAPI 代理地址系列。 这些入口点用于与该驱动程序进行通信。

NDPROXY 可以枚举微型端口驱动程序的 TAPI 功能和更高版本将封装的 TAPI 请求发送 NDIS 结构中。 有关使用 TAPI 支持的 CoNDIS 扩展的详细信息，请参阅[CoNDIS WAN 操作的支持台电话服务](condis-wan-operations-that-support-telephonic-services.md)。

 

 





