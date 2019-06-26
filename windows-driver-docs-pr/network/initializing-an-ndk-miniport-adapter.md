---
title: 初始化 NDK 微型端口适配器
description: 本部分介绍如何初始化 NDK 微型端口适配器
ms.assetid: 0A920057-3C12-4770-BA08-6C3BB24072EB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7cdec770f7ef7b92df0c10dbfc8a9034247c0df1
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67381293"
---
# <a name="initializing-an-ndk-miniport-adapter"></a>初始化 NDK 微型端口适配器


Network Direct 的内核 (NDK) 微型端口适配器初始化其他微型端口适配器相同的方式：NDIS 调用微型端口适配器[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数中所述[初始化微型端口适配器](initializing-a-miniport-adapter.md)。 本主题介绍的微型端口适配器的特定于 NDK 的要求*MiniportInitializeEx*函数。

在其[ *MiniportInitializeEx* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nc-ndis-miniport_initialize)函数，微型端口驱动程序必须执行以下操作：

1.  填充[ **NDIS\_微型端口\_适配器\_NDK\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/ns-ndis-_ndis_miniport_adapter_ndk_attributes)适配器结构，按如下所示：

    - 微型端口驱动程序集**标头**成员的成员说明中所述来标识为支持 NDK 微型端口适配器的适配器。

    - 微型端口驱动程序集**已启用**成员添加到**TRUE**如果启用了其 NDK 功能，或**FALSE**否则为。

        > [!NOTE]
        > 有关查询和设置的当前状态的微型端口驱动程序的 NDK 功能的详细信息，请参阅[启用和禁用 NDK 功能](enabling-and-disabling-ndk-functionality.md)。         

    - 在中**NdkCapabilities**成员，微型端口驱动程序存储一个指向[ **NDIS\_NDK\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ntddndis/ns-ntddndis-_ndis_ndk_capabilities)结构，它指定该适配器的功能。

2.  调用[ **NdisMSetMiniportAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/ndis/nf-ndis-ndismsetminiportattributes)为适配器设置这些属性。

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口 (NDKPI)](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






