---
title: 中间驱动程序中的动态绑定
description: 中间驱动程序中的动态绑定
keywords:
- 中间驱动程序 WDK 网络，绑定
- NDIS 中间驱动程序 WDK，绑定
- 动态绑定 WDK 网络
- 绑定操作 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 91cbd8887a18c3b624181a33f652322d2b58172b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96822997"
---
# <a name="dynamic-binding-in-an-intermediate-driver"></a>中间驱动程序中的动态绑定





中间驱动程序必须通过提供 [*ProtocolBindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_bind_adapter_ex) 和 [*ProtocolUnbindAdapterEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-protocol_unbind_adapter_ex) 函数来支持到基础微型端口适配器的动态绑定。

当微型端口适配器可用时，NDIS 将调用可以绑定到该微型端口适配器的任何中间驱动程序的 *ProtocolBindAdapterEx* 函数。 作为绑定操作的一部分，中间驱动程序应初始化与该小型端口适配器关联的虚拟微型端口。 删除微型端口适配器后，NDIS 会调用绑定到该微型端口适配器的任何中间驱动程序的 *ProtocolUnbindAdapterEx* 函数。

以下主题包含有关中间驱动程序中动态绑定操作的其他信息：

[中间驱动程序绑定操作](intermediate-driver-binding-operations.md)

[打开中间驱动程序下面的适配器](opening-an-adapter-underlying-an-intermediate-driver.md)

[初始化虚拟微型端口](initializing-virtual-miniports.md)

[中间驱动程序取消绑定操作](intermediate-driver-unbinding-operations.md)

 

