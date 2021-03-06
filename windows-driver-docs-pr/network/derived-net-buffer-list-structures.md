---
title: 派生的 NET_BUFFER_LIST 结构
description: 派生的 NET_BUFFER_LIST 结构
keywords:
- NET_BUFFER_LIST
- 网络数据 WDK，结构
- 数据 WDK 网络，结构
- 包 WDK 网络，数据结构
- 派生结构 WDK 网络
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85f0bf6669508dd6ced48044a2ec5781abb016bb
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248048"
---
# <a name="derived-net_buffer_list-structures"></a>派生的网络 \_ 缓冲区 \_ 列表结构





NDIS 提供了一些函数，驱动程序可以使用这些函数来管理从其他网络缓冲区列表结构派生的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 结构 \_ \_ 。 这些函数通常由中间驱动程序使用。

以下 NDIS 函数可以 \_ \_ 从现有的网络 \_ 缓冲区列表结构创建派生的网络缓冲区列表结构 \_ ：

[**NdisAllocateCloneNetBufferList**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisallocateclonenetbufferlist)

[**NdisAllocateFragmentNetBufferList**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisallocatefragmentnetbufferlist)

[**NdisAllocateReassembledNetBufferList**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisallocatereassemblednetbufferlist)

这些函数会提高系统性能，因为 NDIS 在不复制网络数据的情况下创建派生的结构。 有三种类型的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 结构可从现有的网络 \_ 缓冲区 \_ 列表结构派生：

<a href="" id="clone"></a>克隆  
克隆的网络 \_ 缓冲区 \_ 列表结构是一个引用原始数据的重复。 驱动程序可以使用这种类型的结构有效地将相同的数据传输到多个路径。

<a href="" id="fragment"></a>Fragment  
片段 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 结构包含一组引用原始数据的 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer) 结构; 但是，数据被划分为不超过最大大小的单位。 驱动程序可以使用这种类型的结构将大型缓冲区有效地分解为较小的缓冲区。

<a href="" id="reassembled"></a>目的地  
重新组合的网络 \_ 缓冲区 \_ 列表结构包含一个网络 \_ 缓冲区结构，该结构引用多个源网络 \_ 缓冲区结构中的原始数据。 驱动程序可以使用这种类型的结构将很多较小的缓冲区有效地合并为一个大的缓冲区。

以下主题提供了有关派生的网络 \_ 缓冲区列表结构的详细信息 \_ ：

-   [网络 \_ 缓冲区 \_ 列表生成之间的关系](relationships-between-net-buffer-list-generations.md)
-   [克隆的网络 \_ 缓冲区 \_ 列表结构](cloned-net-buffer-list-structures.md)
-   [碎片网络 \_ 缓冲区 \_ 列表结构](fragmented-net-buffer-list-structures.md)
-   [重新组合网络 \_ 缓冲区 \_ 列表结构](reassembled-net-buffer-list-structures.md)

 

