---
title: 内核网络微型重定向程序驱动程序
description: 内核网络微型重定向程序驱动程序
ms.assetid: 13236e5f-1261-4cf1-9c3d-3f1a5ccb3323
keywords:
- 网络重定向程序 WDK，最小重定向程序驱动程序
- 重定向程序驱动程序 WDK，最小化重定向程序驱动程序
- 内核网络重定向程序 WDK，最小重定向程序驱动程序
- 最小重定向程序 WDK
- 最小-重定向程序 WDK，有关内核网络微型重定向程序驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5e1e5466e526e58b9c261b68cdb2d541df3f669e
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354670"
---
# <a name="the-kernel-network-mini-redirector-driver"></a>内核网络微型重定向程序驱动程序


## <span id="ddk_the_kernel_network_mini_redirector_driver_if"></span><span id="DDK_THE_KERNEL_NETWORK_MINI_REDIRECTOR_DRIVER_IF"></span>


内核网络微型重定向程序驱动程序实现多个用于通过重定向驱动器缓冲子系统 (RDBSS) 与该驱动程序进行通信的回调例程。 在此文档的其余部分，内核网络微型重定向程序驱动程序称为网络微型重定向程序驱动程序。

网络微型重定向程序驱动程序的第一次启动 (在其**DriverEntry**例程)，该驱动程序调用 RDBSS [ **RxRegisterMinirdr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxregisterminirdr)例程，以注册网络使用 RDBSS 微型重定向程序驱动程序。 网络微型重定向程序驱动程序传入 MINIRDR\_调度结构，其中包括配置数据以及网络微型重定向程序驱动程序实现 （调度表） 的例程的指针。

可以选择实现的这些例程仅某些网络微型重定向。 由网络微型重定向不实现任何例程应设置为**NULL** MINIRDR 中的指针\_调度结构传递给**RxRegisterMinirdr**。 RDBSS 只会调用由网络微型-重定向程序实现的例程。

由网络微型重定向实现的例程的一个特殊类别是表示传统的文件 I/O 调用的读取、 写入和其他文件操作的低 I/O 操作。 所有较低的 I/O 例程可由 RDBSS 以异步方式调用。 网络微型重定向的内核驱动程序必须进行某些，实现任何低 I/O 例程可以安全地调用以异步方式。 较低的 I/O 例程中作为传递的例程的指针的数组作为一部分 MINIRDR\_调度结构从[ **DriverEntry** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_initialize)例程。 数组项的值是要执行的较低的 I/O 操作。 所有较低的 I/O 例程预期指向 RX\_上下文结构中作为参数进行传递。 RX\_上下文的数据结构具有**LowIoContext.Operation**还指定了要执行的较低的 I/O 操作的成员。 可以为多个较低的 I/O 例程，以指向网络微型重定向程序驱动程序中的相同例程，因为这样**LowIoContext.Operation**成员可用于指定请求的较低的 I/O 操作。 例如，所有与文件锁相关的低 I/O 调用可以在网络微型-重定向程序中调用相同的低 I/O 例程，并可以使用此例程**LowIoContext.Operation**成员指定锁定或解锁的操作请求。

RDBSS 还假定对于少数其他例程由网络微型重定向实现异步操作。 这些例程用于建立与远程资源的连接。 连接操作可能要花费相当长的时间才能完成，因为 RDBSS 假定这些例程实施为异步操作。

RDBSS 假定所有例程由网络微型重定向而不是较低的 I/O 和连接相关的例程实现都基于同步调用。 但是，这是将在未来版本的 Windows 操作系统中进行。

所有由网络微型重定向实现的例程返回上完成的 NTSTATUS 值。 大多数例程将返回状态\_成功或适当的 NTSTATUS 值成功。 除了特定于特殊例程的返回值，还有两个一般类别的大部分例程的返回的错误：

-   网络错误

-   身份验证错误

可能的网络错误包括以下内容：

<span id="STATUS_IO_TIMEOUT"></span><span id="status_io_timeout"></span>状态\_IO\_超时  
对远程服务器的 I/O 请求已超时。

<span id="STATUS_BAD_NETWORK_PATH"></span><span id="status_bad_network_path"></span>状态\_坏\_网络\_路径  
I/O 请求时为不存在的网络路径。 如果目录已重命名或删除，可以发生此错误。

<span id="STATUS_NETWORK_UNREACHABLE"></span><span id="status_network_unreachable"></span>状态\_网络\_不可访问  
从客户端无法访问网络。

<span id="STATUS_REMOTE_NOT_LISTENING"></span><span id="status_remote_not_listening"></span>状态\_远程\_不\_正在侦听  
远程服务器不侦听连接。

<span id="STATUS_USER_SESSION_DELETED"></span><span id="status_user_session_deleted"></span>状态\_用户\_会话\_已删除  
在服务器上的用户会话已被删除。 该会话可能已超时，服务器可能会重新启动导致要删除的所有现有用户会话或服务器上的管理员可能会强制用户会话的删除。

<span id="STATUS_CONNECTION_DISCONNECTED"></span><span id="status_connection_disconnected"></span>状态\_连接\_已断开连接  
与远程服务器的连接已断开连接。

<span id="STATUS_NETWORK_NAME_DELETED"></span><span id="status_network_name_deleted"></span>状态\_网络\_名称\_已删除  
I/O 请求是针对已删除的网络名称。

可能的身份验证错误包括以下内容：

<span id="STATUS_LOGON_FAILURE"></span><span id="status_logon_failure"></span>状态\_登录\_失败  
对远程服务器的登录请求失败。

<span id="STATUS_NETWORK_CREDENTIAL_CONFLICT"></span><span id="status_network_credential_conflict"></span>状态\_网络\_凭据\_冲突  
没有与已提供的网络凭据发生冲突。

<span id="STATUS_DOWNGRADE_DETECTED"></span><span id="status_downgrade_detected"></span>状态\_降级\_检测到  
服务器已检测到客户端用于与服务器通信的网络协议的更改和更改已为旧版本的协议。

<span id="STATUS_LOGIN_WKSTA_RESTRICTION"></span><span id="status_login_wksta_restriction"></span>状态\_登录名\_WKSTA\_限制  
没有限制工作站登录到服务器。

以下各节详细讨论了通过网络微型重定向可以实现的例程：

[由内核网络 Mini-redirector 实现的例程](routines-implemented-by-the-kernel-network-mini-redirector.md)

[不使用 RDBSS 例程](routines-not-used-by-rdbss.md)

由网络微型重定向实现的例程可以归纳为以下类别基于其功能：

[连接和名称解析](connection-and-name-resolution.md)

[驱动程序启动、 停止和设备控制](driver-start--stop--and-device-control.md)

[文件系统对象的创建和删除](file-system-object-creation-and-deletion.md)

[文件系统对象 I/O 例程](file-system-object-i-o-routines.md)

[文件系统对象查询和 Set 例程](file-system-object-query-and-set-routines.md)

[杂项网络微型重定向程序例程](miscellaneous-network-mini-redirector-routines.md)

 

 




