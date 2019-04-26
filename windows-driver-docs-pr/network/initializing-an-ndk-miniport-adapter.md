---
title: 初始化 NDK 微型端口适配器
description: 本部分介绍如何初始化 NDK 微型端口适配器
ms.assetid: 0A920057-3C12-4770-BA08-6C3BB24072EB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c05d90fc4c3d713cdea3ce7581ba0807afcdd2c5
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63324975"
---
# <a name="initializing-an-ndk-miniport-adapter"></a>初始化 NDK 微型端口适配器


Network Direct 的内核 (NDK) 微型端口适配器初始化其他微型端口适配器相同的方式：NDIS 调用微型端口适配器[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数中所述[初始化微型端口适配器](initializing-a-miniport-adapter.md)。 本主题介绍的微型端口适配器的特定于 NDK 的要求*MiniportInitializeEx*函数。

在其[ *MiniportInitializeEx* ](https://msdn.microsoft.com/library/windows/hardware/ff559389)函数，微型端口驱动程序必须执行以下操作：

1.  填充[ **NDIS\_微型端口\_适配器\_NDK\_属性**](https://msdn.microsoft.com/library/windows/hardware/hh451558)适配器结构，按如下所示：

    - 微型端口驱动程序集**标头**成员的成员说明中所述来标识为支持 NDK 微型端口适配器的适配器。

    - 微型端口驱动程序集**已启用**成员添加到**TRUE**如果启用了其 NDK 功能，或**FALSE**否则为。

        > [!NOTE]
        > 有关查询和设置的当前状态的微型端口驱动程序的 NDK 功能的详细信息，请参阅[启用和禁用 NDK 功能](enabling-and-disabling-ndk-functionality.md)。         

    - 在中**NdkCapabilities**成员，微型端口驱动程序存储一个指向[ **NDIS\_NDK\_功能**](https://msdn.microsoft.com/library/windows/hardware/hh451560)结构，它指定该适配器的功能。

2.  调用[ **NdisMSetMiniportAttributes** ](https://msdn.microsoft.com/library/windows/hardware/ff563672)为适配器设置这些属性。

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口 (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






