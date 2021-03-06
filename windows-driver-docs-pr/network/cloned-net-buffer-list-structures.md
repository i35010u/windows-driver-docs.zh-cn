---
title: 克隆的 NET_BUFFER_LIST 结构
description: 克隆的 NET_BUFFER_LIST 结构
keywords:
- NET_BUFFER_LIST
- 克隆的结构 WDK 网络
- 复制结构 WDK 网络
- 父/子 NET_BUFFER_LIST 关系 WDK 网络
- 子/父 NET_BUFFER_LIST 关系 WDK 网络
- 关系 WDK NET_BUFFER_LIST
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2f1e779445504c899de7cc32187705cda8e57134
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102248678"
---
# <a name="cloned-net_buffer_list-structures"></a>克隆的网络 \_ 缓冲区 \_ 列表结构





NDIS 驱动程序根据现有的网络缓冲区列表结构创建克隆的 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 结构 \_ \_ 。 克隆的结构引用原始结构数据。 驱动程序可以使用这种类型的结构有效地将相同的数据传输到多个路径。

下图显示了父网络 \_ 缓冲区 \_ 列表结构和克隆的子结构之间的关系。

![说明父网络 \- 缓冲区 \- 列表结构和克隆的子结构之间的关系的关系图](images/netbufferlistclone.png)

上图包含一个父 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 结构和一个派生自该父级的子结构。 父结构具有一个 [**网络 \_ 缓冲区 \_ 列表 \_ 上下文**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list_context) 结构和一个附加了 MDLs 的 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer) 结构。 父结构的父指针为 **NULL** ，表示它不是派生的结构。

子网络 \_ 缓冲区 \_ 列表结构具有一个 \_ 附加了 MDLs 的网络缓冲区结构。 子网络 \_ 缓冲区 \_ 列表包含指向父结构的指针。 如果网络 \_ 缓冲区 \_ 列表 \_ 上下文指针为 NULL，则表示子级没有网络 \_ 缓冲区 \_ 列表 \_ 上下文结构。

驱动程序调用 [**NdisAllocateCloneNetBufferList**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisallocateclonenetbufferlist) 函数来创建克隆 [**网络 \_ 缓冲区 \_ 列表**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list) 结构。 NDIS 用克隆的网络缓冲区列表结构分配新的 [**网络 \_ 缓冲区**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer) 结构和 MDLs \_ \_ 。 对于克隆的结构，NDIS 不分配 [**网络 \_ 缓冲区 \_ 列表 \_ 上下文**](/windows-hardware/drivers/ddi/nbl/ns-nbl-net_buffer_list_context) 结构。 新的 NET \_ BUFFER 结构和 MDLs 描述与父结构相同的数据。 不会复制数据。

驱动程序调用 [**NdisFreeCloneNetBufferList**](/windows-hardware/drivers/ddi/nblapi/nf-nblapi-ndisfreeclonenetbufferlist) 函数，以释放网络 \_ 缓冲区 \_ 列表结构以及所有关联的网络 \_ 缓冲区结构和 MDL 链，这些链以前通过调用 **NdisAllocateCloneNetBufferList** 分配。

## <a name="related-topics"></a>相关主题


[派生的网络 \_ 缓冲区 \_ 列表结构](derived-net-buffer-list-structures.md)

 

