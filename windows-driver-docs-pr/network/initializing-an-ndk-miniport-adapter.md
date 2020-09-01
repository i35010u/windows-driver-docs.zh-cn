---
title: 初始化 NDK 微型端口适配器
description: 本部分介绍如何初始化 NDK 微型端口适配器
ms.assetid: 0A920057-3C12-4770-BA08-6C3BB24072EB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0ec206d7f65506f487f30c78e674190483d943f5
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89216614"
---
# <a name="initializing-an-ndk-miniport-adapter"></a>初始化 NDK 微型端口适配器


使用与其他微型端口适配器相同的方式初始化网络直接内核 (NDK) 微型端口适配器： NDIS 调用微型端口适配器的 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数，如 [初始化微型端口适配器](initializing-a-miniport-adapter.md)中所述。 本主题介绍了微型端口适配器的 *MiniportInitializeEx* 函数的特定于 NDK 的要求。

在 [*MiniportInitializeEx*](/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize) 函数中，微型端口驱动程序必须执行以下操作：

1.  按如下方式为适配器填充 [**NDIS \_ 微型端口 \_ 适配器 \_ NDK \_ 属性**](/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_ndk_attributes) 结构：

    - 微型端口驱动程序设置 **标头** 成员，如成员说明中所述，将适配器标识为支持 NDK 的小型端口适配器。

    - 如果启用 **的成员启用** 了该成员的 NDK 功能，则该驱动程序会将该成员设置为 **TRUE** ，否则设置为 **FALSE** 。

        > [!NOTE]
        > 有关查询和设置微型端口驱动程序 NDK 功能的当前状态的详细信息，请参阅 [启用和禁用 Ndk 功能](enabling-and-disabling-ndk-functionality.md)。         

    - 在 **NdkCapabilities** 成员中，微型端口驱动程序存储一个指向 [**NDIS \_ NDK \_ 功能**](/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ndk_capabilities) 结构的指针，该结构指定适配器的功能。

2.  调用 [**NdisMSetMiniportAttributes**](/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes) 为适配器设置这些属性。

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口 (NDKPI)](./overview-of-network-direct-kernel-provider-interface--ndkpi-.md)

 

