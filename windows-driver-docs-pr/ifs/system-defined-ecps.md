---
title: 系统定义的 ECP
description: 系统定义的 ECP
ms.assetid: 6acb4be4-a7aa-431d-b2d8-3ef6d41cb4ef
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ac469ec4aa9ba4a01becb9df50aa5a78fdd5a0ca
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89063230"
---
# <a name="system-defined-ecps"></a>系统定义的 ECP


操作系统在 *Ntifs* 头文件中定义了以下 ECPs。 这些系统定义的 ECPs 将指定的额外信息附加到文件上的 [**IRP \_ MJ \_ CREATE**](./irp-mj-create.md) 操作。 文件系统堆栈的元素可查询 ECPs 以获取其他信息。

通常，在文件上处理 [**IRP \_ mj \_ CREATE**](./irp-mj-create.md) 操作的筛选器，然后将文件向下传递到下面的筛选器，而不能将以下系统定义的 ECPs 附加到该文件上的 **irp \_ mj \_ create** 操作并进行欺骗。 同样，处理和颁发 IRP mj create 操作的内核模式驱动程序 \_ \_ 不得将以下系统定义的 ECPs 附加到 irp \_ mj 创建操作，并对文件进行欺骗 \_ 。 以下系统定义的 ECPs 为只读。 只应使用它们来检索信息。

限制筛选器驱动程序附加任何系统定义的 ECPs 的例外是筛选器驱动程序实现分层文件系统。 它通过拥有文件对象并在其筛选器下的文件上颁发自己的 [**irp \_ mj \_ create**](./irp-mj-create.md) 操作来实现此操作，以响应对 \_ \_ 筛选器驱动程序服务在其自己的文件对象上的文件的 irp mj create 操作。 此类筛选器驱动程序应将任何 ecp 上下文结构 (列表 \_ 从文件上的原始 IRP \_ mj create 操作) 从文件上的原始 IRP mj \_ create 操作传播到 IRP \_ mj \_ create 操作，筛选器驱动程序会在其下遇到问题。 通过传播这些 ECP 列表，筛选器驱动程序可确保用于颁发 IRP mj 创建操作的筛选器下的任何筛选器 \_ \_ 都知道原始 IRP \_ mj \_ 创建操作的上下文。

<span id="GUID_ECP_OPLOCK_KEY"></span><span id="guid_ecp_oplock_key"></span>GUID \_ ECP \_ OPLOCK \_ 密钥  
标识 [**oplock \_ 键 \_ ECP \_ 上下文**](./oplock-key-ecp-context.md) 结构的 GUID，用于将 oplock 密钥附加到打开的文件请求。 使用 oplock 键，应用程序可以在不中断应用程序自身 oplock 的情况下，在同一流中打开多个句柄。

有关 oplock 和 oplock 密钥的详细信息，请参阅 [Oplock 语义概述](oplock-overview.md)。

<span id="GUID_ECP_NETWORK_OPEN_CONTEXT"></span><span id="guid_ecp_network_open_context"></span>GUID \_ ECP \_ 网络 \_ 打开 \_ 上下文  
标识 [**网络 \_ 开放 \_ ECP \_ 上下文**](/previous-versions/ff550896(v=vs.85)) 结构的 GUID，用于附加网络重定向器的额外信息。 此 GUID 还为在 windows 7 及更高版本的 Windows 上运行的驱动程序以及必须解释位于 Windows Vista 上的文件上的网络 ECP 上下文的驱动程序标识 [**网络 \_ 开放 \_ ECP \_ 上下文 \_ V0**](/previous-versions/ff550899(v=vs.85)) 结构。

<span id="GUID_ECP_PREFETCH_OPEN"></span><span id="guid_ecp_prefetch_open"></span>GUID \_ ECP \_ 预提取 \_ 打开  
标识 [**预提取的 \_ 开放 \_ ECP \_ 上下文**](/previous-versions/ff551843(v=vs.85)) 结构的 GUID。

Prefetcher 是操作系统的一个组件，它与缓存管理器和内存管理器紧密集成，使磁盘访问更高效，从而提高性能。 如果其他组件干扰 prefetcher，系统性能会下降，可能会死锁。 因此，prefetcher 会将预提取的 \_ 开放式 \_ ECP \_ 上下文结构附加到一个文件中，以便与 prefetcher 对该文件执行打开的请求进行通信。 此打开请求由预提取的**Context**已 \_ 打开 \_ ECP 上下文的上下文成员指定 \_ 。 其他组件（如文件系统筛选器驱动程序）可以确定是否已将预取 \_ 开放式 \_ ECP \_ 上下文附加到文件，然后采取相应的操作。

<span id="GUID_ECP_NFS_OPEN"></span><span id="guid_ecp_nfs_open"></span>GUID \_ ECP \_ NFS \_ 打开  
标识 [**NFS \_ 开放 \_ ECP \_ 上下文**](/previous-versions/ff550942(v=vs.85)) 结构的 GUID。 网络文件系统 (NFS) 服务器将 NFS \_ 开放 \_ ECP \_ 上下文结构附加到打开的文件请求。 NFS 服务器对 NFS 服务器为满足客户端请求而进行的任何打开的文件请求使用此 GUID。 然后，文件系统堆栈可以确定是否已将 \_ NFS \_ 打开 \_ 的 ECP 上下文附加到打开的文件请求。 基于 NFS \_ 打开 ECP 上下文中的 \_ 信息 \_ ，文件系统堆栈可以确定请求打开文件的客户端和原因。

<span id="GUID_ECP_SRV_OPEN"></span><span id="guid_ecp_srv_open"></span>GUID \_ ECP \_ SRV \_ 打开  
标识 [**SRV \_ 开放 \_ ECP \_ 上下文**](/previous-versions/ff556749(v=vs.85)) 结构的 GUID。 服务器将 SRV \_ 开放 \_ ECP \_ 上下文结构附加到打开的文件请求。 服务器对任何打开的文件请求使用此 GUID，服务器将该请求用于满足条件客户端请求。 然后，文件系统堆栈可以确定是否已将 SRV \_ 开放式 \_ ECP \_ 上下文附加到打开的文件请求。 基于 SRV \_ 开放 ECP 上下文中的 \_ 信息 \_ ，文件系统堆栈可以确定请求打开文件的客户端和原因。

<span id="GUID_ECP_DUAL_OPLOCK_KEY"></span><span id="guid_ecp_dual_oplock_key"></span>GUID \_ ECP \_ 双重 \_ OPLOCK \_ 键  
标识 [**双 OPLOCK \_ 密钥 \_ ECP \_ 上下文**](./dual-oplock-key-ecp-context.md) 结构的 GUID。 与 [**oplock \_ key \_ ecp \_ 上下文**](./oplock-key-ecp-context.md) 结构一样， **双 oplock \_ 键 \_ ecp \_ 上下文** 用于将 OPLOCK 密钥附加到打开的文件请求。 然而，使用 **双重 OPLOCK \_ 键 \_ ECP \_ 上下文**时，还可以设置父键来为目标文件的目录提供 OPLOCK。

<span id="GUID_ECP_IO_DEVICE_HINT"></span><span id="guid_ecp_io_device_hint"></span>GUID \_ ECP \_ IO \_ 设备 \_ 提示  
标识 **IO \_ 设备 \_ 提示 \_ ECP \_ 上下文** 结构的 GUID。 设备提示用于帮助提供名称提供程序微筛选器驱动程序，以便将重分析目标跟踪到新设备。

<span id="GUID_ECP_NETWORK_APP_INSTANCE"></span><span id="guid_ecp_network_app_instance"></span>GUID \_ ECP \_ 网络 \_ 应用 \_ 实例  
标识 [**网络 \_ 应用 \_ 实例 \_ ECP \_ 上下文**](/previous-versions/hh439443(v=vs.85)) 结构的 GUID。 故障转移群集中的客户端应用程序可能会在群集中的节点上打开一组文件。 文件对象通过 **网络 \_ 应用 \_ 实例 \_ ECP \_ 上下文** 结构中的实例标识符标记为应用程序。 故障转移时，辅助节点可以使用以前缓存的应用程序实例标识符验证客户端应用程序对已打开文件的访问权限。

 

