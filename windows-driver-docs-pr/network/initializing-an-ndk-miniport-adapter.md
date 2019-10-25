---
title: 初始化 NDK 微型端口适配器
description: 本部分介绍如何初始化 NDK 微型端口适配器
ms.assetid: 0A920057-3C12-4770-BA08-6C3BB24072EB
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06b4c8bd7cc6d96073bc145b36fe032f960da97b
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72824494"
---
# <a name="initializing-an-ndk-miniport-adapter"></a>初始化 NDK 微型端口适配器


网络直通内核（NDK）微型端口适配器的初始化方式与其他微型端口适配器相同： NDIS 调用微型端口适配器的[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数，如[初始化微型端口适配器](initializing-a-miniport-adapter.md)中所述。 本主题介绍了微型端口适配器的*MiniportInitializeEx*函数的特定于 NDK 的要求。

在[*MiniportInitializeEx*](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nc-ndis-miniport_initialize)函数中，微型端口驱动程序必须执行以下操作：

1.  按如下所示，将[**NDIS\_微型端口\_适配器\_NDK\_属性**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/ns-ndis-_ndis_miniport_adapter_ndk_attributes)结构：

    - 微型端口驱动程序设置**标头**成员，如成员说明中所述，将适配器标识为支持 NDK 的小型端口适配器。

    - 如果启用**的成员启用**了该成员的 NDK 功能，则该驱动程序会将该成员设置为**TRUE** ，否则设置为**FALSE** 。

        > [!NOTE]
        > 有关查询和设置微型端口驱动程序 NDK 功能的当前状态的详细信息，请参阅[启用和禁用 Ndk 功能](enabling-and-disabling-ndk-functionality.md)。         

    - 在**NdkCapabilities**成员中，微型端口驱动程序存储一个指向[**NDIS\_NDK\_功能**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddndis/ns-ntddndis-_ndis_ndk_capabilities)结构的指针，该结构指定适配器的功能。

2.  调用[**NdisMSetMiniportAttributes**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ndis/nf-ndis-ndismsetminiportattributes)为适配器设置这些属性。

## <a name="related-topics"></a>相关主题


[网络直接内核提供程序接口（NDKPI）](network-direct-kernel-programming-interface--ndkpi-.md)

 

 






