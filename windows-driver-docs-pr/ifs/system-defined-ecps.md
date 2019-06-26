---
title: 系统定义的 ECP
description: 系统定义的 ECP
ms.assetid: 6acb4be4-a7aa-431d-b2d8-3ef6d41cb4ef
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 24ea2cd09d4295e932faca4413802c036e2e840d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67371309"
---
# <a name="system-defined-ecps"></a>系统定义的 ECP


操作系统定义中的以下 ECPs *Ntifs.h*标头文件。 这些系统定义 ECPs 附加到指定的额外信息[ **IRP\_MJ\_创建**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)文件中的操作。 文件系统堆栈中的元素可以查询有关的额外信息 ECPs。

通常情况下，筛选器的处理[ **IRP\_MJ\_创建**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)上一个文件，然后传递到其下面的筛选器的文件必须不附加和欺骗的以下任何操作系统定义的到 ECPs **IRP\_MJ\_创建**文件上的操作。 同样的内核模式驱动程序处理，并发布 IRP\_MJ\_对文件的创建操作必须不附加和欺骗任何 IRP 到以下系统定义 ECPs\_MJ\_创建操作文件。 以下系统定义 ECPs 是只读的。 应使用它们来检索信息仅供参考。

附加任何以下系统定义 ECPs 限制筛选器驱动程序的一个例外是当筛选器驱动程序实现分层的文件系统。 通过拥有文件对象，通过发出其自己做到这一点[ **IRP\_MJ\_创建**](https://docs.microsoft.com/windows-hardware/drivers/ifs/irp-mj-create)对其筛选器，以响应 IRP 将以下文件的操作\_MJ\_筛选器驱动程序服务在其自己的文件对象的文件上创建操作。 这样的筛选器驱动程序应传播任何 ECP 上下文结构列表 (ECP\_列表) 从原始 IRP\_MJ\_IRP 到文件的创建操作\_MJ\_创建操作的筛选器驱动程序它下面的问题。 通过将传播这些 ECP 列表，筛选器驱动程序确保如下颁发 IRP 的筛选器的任何筛选器\_MJ\_创建操作的原始 IRP 上下文的可识别\_MJ\_创建操作。

<span id="GUID_ECP_OPLOCK_KEY"></span><span id="guid_ecp_oplock_key"></span>GUID\_ECP\_OPLOCK\_密钥  
标识的 GUID [ **OPLOCK\_密钥\_ECP\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ifs/oplock-key-ecp-context)结构，用于将 oplock 密钥附加到打开的文件请求。 Oplock 密钥允许应用程序而不会中断应用程序自身 oplock 打开相同流到多个句柄。

有关 oplock 和 oplock 密钥的详细信息，请参阅[Oplock 语义概述](overview.md)。

<span id="GUID_ECP_NETWORK_OPEN_CONTEXT"></span><span id="guid_ecp_network_open_context"></span>GUID\_ECP\_网络\_打开\_上下文  
标识的 GUID [**网络\_打开\_ECP\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff550896)结构，用于将附加网络重定向程序的其他信息。 此 GUID 还标识[**网络\_打开\_ECP\_上下文\_V0** ](https://msdn.microsoft.com/library/windows/hardware/ff550899)在 Windows 7 和更高版本运行的驱动程序的结构Windows，必须将驻留在 Windows Vista 的文件上的网络 ECP 上下文解释。

<span id="GUID_ECP_PREFETCH_OPEN"></span><span id="guid_ecp_prefetch_open"></span>GUID\_ECP\_预提取\_打开  
标识的 GUID [**预提取\_打开\_ECP\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff551843)结构。

取是操作系统的与缓存管理器和内存管理器来提高效率的磁盘访问并因此提高性能紧密集成的组件。 如果其他组件会干扰取，系统性能降低并可能死锁。 因此，取附加预提取\_打开\_ECP\_上下文结构到要进行通信，对取的文件执行打开请求的文件。 指定此打开请求**上下文**预提取的成员\_打开\_ECP\_上下文。 其他组件，例如，文件系统筛选器驱动程序中，可以确定是否预提取\_开放\_ECP\_上下文附加到文件，然后采取适当的措施。

<span id="GUID_ECP_NFS_OPEN"></span><span id="guid_ecp_nfs_open"></span>GUID\_ECP\_NFS\_OPEN  
标识的 GUID [ **NFS\_打开\_ECP\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff550942)结构。 网络文件系统 (NFS) 服务器将附加 NFS\_打开\_ECP\_上下文结构到打开的文件请求。 NFS 服务器上的 NFS 服务器可满足客户端请求的任何打开的文件请求使用此 GUID。 文件系统堆栈就可以确定是否 NFS\_打开\_ECP\_上下文附加到打开的文件请求。 基于 NFS 中的信息\_开放\_ECP\_上下文的文件系统堆栈可以确定客户端请求打开文件和原因。

<span id="GUID_ECP_SRV_OPEN"></span><span id="guid_ecp_srv_open"></span>GUID\_ECP\_SRV\_打开  
标识的 GUID [ **SRV\_打开\_ECP\_上下文**](https://msdn.microsoft.com/library/windows/hardware/ff556749)结构。 服务器将附加 SRV\_打开\_ECP\_上下文结构到打开的文件请求。 服务器上任何打开的文件请求的服务器可满足条件的客户端请求使用此 GUID。 文件系统堆栈就可以确定是否 SRV\_打开\_ECP\_上下文附加到打开的文件请求。 基于 SRV 中的信息\_开放\_ECP\_上下文的文件系统堆栈可以确定客户端请求打开文件和原因。

<span id="GUID_ECP_DUAL_OPLOCK_KEY"></span><span id="guid_ecp_dual_oplock_key"></span>GUID\_ECP\_双\_OPLOCK\_密钥  
标识的 GUID [**双 OPLOCK\_密钥\_ECP\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ifs/dual-oplock-key-ecp-context)结构。 像[ **OPLOCK\_密钥\_ECP\_上下文**](https://docs.microsoft.com/windows-hardware/drivers/ifs/oplock-key-ecp-context)结构**双 OPLOCK\_键\_ECP\_上下文**用于将 oplock 密钥附加到打开的文件请求。 与**双 OPLOCK\_密钥\_ECP\_上下文**，但是，还可以设置父项为目标文件的目录提供机会锁。

<span id="GUID_ECP_IO_DEVICE_HINT"></span><span id="guid_ecp_io_device_hint"></span>GUID\_ECP\_IO\_设备\_提示  
标识的 GUID **IO\_设备\_提示\_ECP\_上下文**结构。 使用设备提示以帮助跟踪对新设备的重新分析目标名称提供程序微筛选器驱动程序。

<span id="GUID_ECP_NETWORK_APP_INSTANCE"></span><span id="guid_ecp_network_app_instance"></span>GUID\_ECP\_NETWORK\_APP\_INSTANCE  
标识的 GUID [**网络\_应用\_实例\_ECP\_上下文**](https://msdn.microsoft.com/library/windows/hardware/hh439443)结构。 故障转移群集中的客户端应用程序可能具有一组在群集中的节点上打开的文件。 文件对象标记为应用程序通过中的实例标识符**网络\_应用程序\_实例\_ECP\_上下文**结构。 故障转移时，辅助节点可以验证对以前缓存的应用程序实例标识符与打开的文件的客户端应用程序的访问。

 

 




