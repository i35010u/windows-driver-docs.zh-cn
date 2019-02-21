---
title: 中间的驱动程序中动态绑定
description: 中间的驱动程序中动态绑定
ms.assetid: 0b825141-2a19-40c6-82cf-8e897a25b0aa
keywords:
- 中间驱动程序 WDK 网络、 绑定
- NDIS 中间驱动程序 WDK、 绑定
- 动态绑定 WDK 网络
- 绑定操作 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: db7d6ac50dfa604f9ffe8392ac291a3c60239602
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554434"
---
# <a name="dynamic-binding-in-an-intermediate-driver"></a>中间的驱动程序中动态绑定





中间的驱动程序必须通过提供同时支持动态绑定到基础微型端口适配器[ *ProtocolBindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570220)和一个[ *ProtocolUnbindAdapterEx* ](https://msdn.microsoft.com/library/windows/hardware/ff570278)函数。

当微型端口适配器可用时，会调用 NDIS *ProtocolBindAdapterEx*函数可以将绑定到该微型端口适配器任何中间驱动程序。 绑定操作的一部分，中间驱动程序应初始化与该微型端口适配器相关联的虚拟微型端口。 微型端口适配器中删除时，将调用 NDIS *ProtocolUnbindAdapterEx*函数绑定到该微型端口适配器任何中间驱动程序。

以下主题包含有关中间驱动程序中动态绑定操作的其他信息：

[中间驱动程序绑定操作](intermediate-driver-binding-operations.md)

[打开基础中间驱动程序的适配器](opening-an-adapter-underlying-an-intermediate-driver.md)

[初始化虚拟微型端口](initializing-virtual-miniports.md)

[取消绑定操作的中间驱动程序](intermediate-driver-unbinding-operations.md)

 

 





