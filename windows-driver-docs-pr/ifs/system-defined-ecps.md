---
title: 系统定义的 ECP
description: 系统定义的 ECP
ms.assetid: 6acb4be4-a7aa-431d-b2d8-3ef6d41cb4ef
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 85b9b23152e693824c6f0092315e8074762a571a
ms.sourcegitcommit: 8c898615009705db7633649a51bef27a25d72b26
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/07/2020
ms.locfileid: "78910471"
---
# <a name="system-defined-ecps"></a>系统定义的 ECP


操作系统在*Ntifs*头文件中定义了以下 ECPs。 这些系统定义的 ECPs 将指定的额外信息附加到[**IRP\_MJ\_** ](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)对文件创建操作。 文件系统堆栈的元素可查询 ECPs 以获取其他信息。

通常情况下，一个筛选器处理[**IRP\_MJ\_** ](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)在文件上创建操作，然后将该文件向下传递到下面的筛选器，而不能将以下系统定义的 ECPs 附加到**IRP\_MJ\_** 在该文件上创建操作。 同样，处理和颁发 IRP\_MJ\_创建操作的内核模式驱动程序不得将以下系统定义的 ECPs 附加到 IRP\_MJ\_对文件进行创建操作。 以下系统定义的 ECPs 为只读。 只应使用它们来检索信息。

限制筛选器驱动程序附加任何系统定义的 ECPs 的例外是筛选器驱动程序实现分层文件系统。 它通过拥有文件对象并在其筛选器上颁发自己的[**IRP\_MJ\_CREATE**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)操作来执行此操作，以响应 IRP\_\_为其自己的文件对象上的筛选器驱动程序服务的文件创建操作。 此类筛选器驱动程序应将任何 ECP 上下文结构列表（ECP\_列表）从原始 IRP\_MJ\_创建操作传播到 IRP\_MJ\_创建筛选器驱动程序所颁发的操作。 通过传播这些 ECP 列表，筛选器驱动程序可确保筛选器下的任何筛选器\_MJ\_创建操作的筛选器都知道原始 IRP\_MJ\_创建操作的上下文。

<span id="GUID_ECP_OPLOCK_KEY"></span><span id="guid_ecp_oplock_key"></span>GUID\_ECP\_OPLOCK\_键  
标识[**oplock\_密钥\_ECP\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ifs/oplock-key-ecp-context)结构并用于将 oplock 密钥附加到打开的文件请求的 GUID。 使用 oplock 键，应用程序可以在不中断应用程序自身 oplock 的情况下，在同一流中打开多个句柄。

有关 oplock 和 oplock 密钥的详细信息，请参阅[Oplock 语义概述](oplock-overview.md)。

<span id="GUID_ECP_NETWORK_OPEN_CONTEXT"></span><span id="guid_ecp_network_open_context"></span>GUID\_ECP\_网络\_打开\_上下文  
标识[**网络\_打开\_ECP\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff550896)结构的 GUID，用于附加网络重定向器的额外信息。 此 GUID 还会为在 windows 7 及更高版本的 Windows 上运行的驱动程序以及必须解释位于 Windows Vista 上的文件上的网络 ECP 上下文的驱动程序[ **\_打开\_ECP\_上下文\_V0**](https://msdn.microsoft.com/library/windows/hardware/ff550899)结构。

<span id="GUID_ECP_PREFETCH_OPEN"></span><span id="guid_ecp_prefetch_open"></span>GUID\_ECP\_预提取\_打开  
标识[**预提取\_打开\_ECP\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff551843)结构的 GUID。

Prefetcher 是操作系统的一个组件，它与缓存管理器和内存管理器紧密集成，使磁盘访问更高效，从而提高性能。 如果其他组件干扰 prefetcher，系统性能会下降，可能会死锁。 因此，prefetcher 会将\_ECP\_上下文结构中的预提取\_附加到文件，以便在文件上传递 prefetcher 执行打开的请求。 此打开请求由预提取\_打开\_ECP\_上下文的**上下文**成员指定。 其他组件（如文件系统筛选器驱动程序）可以确定是否已将预提取\_打开\_ECP\_上下文附加到文件，然后采取相应的操作。

<span id="GUID_ECP_NFS_OPEN"></span><span id="guid_ecp_nfs_open"></span>GUID\_ECP\_NFS\_打开  
标识[**NFS\_打开\_ECP\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff550942)结构的 GUID。 网络文件系统（NFS）服务器将\_打开\_ECP\_上下文结构附加到打开的文件请求。 NFS 服务器对 NFS 服务器为满足客户端请求而进行的任何打开的文件请求使用此 GUID。 然后，文件系统堆栈可以确定 NFS\_打开\_ECP\_上下文是否已附加到打开的文件请求。 基于 NFS 中的信息\_打开\_ECP\_上下文文件系统堆栈可以确定请求打开文件的客户端和原因。

<span id="GUID_ECP_SRV_OPEN"></span><span id="guid_ecp_srv_open"></span>GUID\_ECP\_SRV\_打开  
标识[**SRV\_打开\_ECP\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff556749)结构的 GUID。 服务器将\_打开的 SRV\_ECP\_上下文结构附加到打开的文件请求。 服务器对任何打开的文件请求使用此 GUID，服务器将该请求用于满足条件客户端请求。 然后，文件系统堆栈可以确定是否已将 SRV\_打开\_ECP\_上下文附加到打开的文件请求。 根据 SRV\_打开\_ECP\_上下文中的信息，文件系统堆栈可以确定请求打开文件的客户端和原因。

<span id="GUID_ECP_DUAL_OPLOCK_KEY"></span><span id="guid_ecp_dual_oplock_key"></span>GUID\_ECP\_双\_OPLOCK\_键  
标识[**双 OPLOCK\_键\_ECP\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ifs/dual-oplock-key-ecp-context)结构的 GUID。 与[**OPLOCK\_密钥\_ecp\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ifs/oplock-key-ecp-context)结构一样，**双 OPLOCK\_密钥\_ecp\_上下文**用于将 OPLOCK 密钥附加到打开的文件请求。 不过，通过**双 OPLOCK\_键\_ECP\_上下文**，也可以设置父键，为目标文件的目录提供 OPLOCK。

<span id="GUID_ECP_IO_DEVICE_HINT"></span><span id="guid_ecp_io_device_hint"></span>GUID\_ECP\_IO\_设备\_提示  
标识**IO\_设备\_提示\_ECP\_上下文**结构的 GUID。 设备提示用于帮助提供名称提供程序微筛选器驱动程序，以便将重分析目标跟踪到新设备。

<span id="GUID_ECP_NETWORK_APP_INSTANCE"></span><span id="guid_ecp_network_app_instance"></span>GUID\_ECP\_网络\_应用\_实例  
标识[**网络\_应用\_实例\_ECP\_上下文**](https://msdn.microsoft.com/library/windows/hardware/hh439443)结构的 GUID。 故障转移群集中的客户端应用程序可能会在群集中的节点上打开一组文件。 文件对象通过**网络\_应用\_实例**中的实例标识符标记为应用程序\_ECP\_上下文结构。 故障转移时，辅助节点可以使用以前缓存的应用程序实例标识符验证客户端应用程序对已打开文件的访问权限。

 

 




