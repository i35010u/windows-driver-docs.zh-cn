---
title: 内核网络微型重定向程序驱动程序
description: 内核网络微型重定向程序驱动程序
ms.assetid: 13236e5f-1261-4cf1-9c3d-3f1a5ccb3323
keywords:
- 网络重定向程序 WDK，最小重定向器驱动程序
- 重定向程序驱动程序 WDK，微型重定向程序驱动程序
- 内核网络重定向 WDK，最小重定向器驱动程序
- 小型重定向程序 WDK
- 小型重定向程序 WDK，关于内核网络小型重定向器驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7959d1f701c7ece79d48b41bffa91e88c3bd7ef0
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065512"
---
# <a name="the-kernel-network-mini-redirector-driver"></a>内核网络微型重定向程序驱动程序


## <span id="ddk_the_kernel_network_mini_redirector_driver_if"></span><span id="DDK_THE_KERNEL_NETWORK_MINI_REDIRECTOR_DRIVER_IF"></span>


内核网络微型重定向程序驱动程序实现了多个回调例程，这些例程由重定向的驱动器缓冲子系统 (RDBSS) 用于与驱动程序通信。 在本文档的其余部分中，内核网络微型重定向程序驱动程序将被称为网络小型重定向程序驱动程序。

当网络微型重定向程序驱动程序首次开始 (在其 **DriverEntry** 例程) 中时，驱动程序将调用 RDBSS [**RxRegisterMinirdr**](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxregisterminirdr) 例程来向 RDBSS 注册网络小型重定向器驱动程序。 网络小型重定向器驱动程序传入 MINIRDR \_ 调度结构，其中包括配置数据和指向网络微型重定向程序驱动程序实现的例程的指针)  (调度表。

网络小型重定向程序可以选择仅实现其中一些例程。 不是由网络小型重定向程序实现的任何例程都应在传递到 RxRegisterMinirdr 的 MINIRDR 调度结构中设置为**NULL**指针 \_ 。 **RxRegisterMinirdr** RDBSS 将仅调用由网络小型重定向程序实现的例程。

由网络小型重定向程序实现的一种特殊类型的例程是低 i/o 操作，表示用于读取、写入和其他文件操作的传统文件 i/o 调用。 所有低 i/o 例程均可通过 RDBSS 异步调用。 网络小型重定向器的内核驱动程序必须确保可以安全地以异步方式调用任何实现的低 i/o 例程。 低 i/o 例程作为例程指针的数组传入，作为 \_ 来自 [**DriverEntry**](/windows-hardware/drivers/ddi/wdm/nc-wdm-driver_initialize) 例程的 MINIRDR 调度结构的一部分。 数组项的值是要执行的低 i/o 操作。 所有低 i/o 例程都需要一个指向 RX \_ 上下文结构的指针作为参数传入。 RX \_ 上下文数据结构具有 **LowIoContext** 成员，该成员还指定要执行的低 i/o 操作。 由于可以使用此 **LowIoContext** 成员来指定请求的低 i/o 操作，因此几个低 i/o 例程可能会指向网络小型重定向程序驱动程序中的同一例程。 例如，所有与文件锁相关的低 i/o 调用都可以在网络小型重定向程序中调用相同的低 i/o 例程，此例程可以使用 **LowIoContext** 成员来指定所请求的锁定或解除锁定操作。

RDBSS 还假设异步操作适用于由网络微型重定向程序实现的几个其他例程。 这些例程用于建立与远程资源的连接。 由于连接操作可能需要很长的时间才能完成，RDBSS 假定将这些例程作为异步操作实现。

RDBSS 假定网络小型重定向程序（而不是低 i/o 和连接相关的例程）实现的所有例程都基于同步调用。 但是，这可能会在将来版本的 Windows 操作系统中发生更改。

网络微重定向程序实现的所有例程在完成时返回一个 NTSTATUS 值。 大多数例程会成功返回状态 \_ success 或适当的 NTSTATUS 值。 除了返回特定于特定例程的值外，对于大多数例程，还可以返回两种常见的错误类别：

-   网络错误

-   身份验证错误

可能的网络错误包括：

<span id="STATUS_IO_TIMEOUT"></span><span id="status_io_timeout"></span>状态 \_ IO \_ 超时  
向远程服务器发出的 i/o 请求已超时。

<span id="STATUS_BAD_NETWORK_PATH"></span><span id="status_bad_network_path"></span>状态 \_ 错误的 \_ 网络 \_ 路径  
I/o 请求指向不存在的网络路径。 如果目录已被重命名或删除，则会出现此错误。

<span id="STATUS_NETWORK_UNREACHABLE"></span><span id="status_network_unreachable"></span>状态 \_ 网络 \_ 无法访问  
无法从客户端访问网络。

<span id="STATUS_REMOTE_NOT_LISTENING"></span><span id="status_remote_not_listening"></span>状态 \_ 远程 \_ 未 \_ 侦听  
远程服务器未侦听连接。

<span id="STATUS_USER_SESSION_DELETED"></span><span id="status_user_session_deleted"></span>\_ \_ 已删除状态用户会话 \_  
已删除服务器上的用户会话。 此会话可能已超时，服务器可能已重新启动，导致删除所有现有用户会话，或者服务器上的管理员可能已强制删除用户会话。

<span id="STATUS_CONNECTION_DISCONNECTED"></span><span id="status_connection_disconnected"></span>状态 \_ 连接已 \_ 断开连接  
与远程服务器的连接已断开。

<span id="STATUS_NETWORK_NAME_DELETED"></span><span id="status_network_name_deleted"></span>\_ \_ 已删除状态网络名称 \_  
I/o 请求适用于已删除的网络名称。

可能的身份验证错误包括：

<span id="STATUS_LOGON_FAILURE"></span><span id="status_logon_failure"></span>状态 \_ 登录 \_ 失败  
对远程服务器的登录请求失败。

<span id="STATUS_NETWORK_CREDENTIAL_CONFLICT"></span><span id="status_network_credential_conflict"></span>状态 \_ 网络 \_ 凭据 \_ 冲突  
出现与提供的网络凭据冲突。

<span id="STATUS_DOWNGRADE_DETECTED"></span><span id="status_downgrade_detected"></span>\_ \_ 检测到状态降级  
服务器检测到客户端用于与服务器进行通信的网络协议的更改，而更改为较旧版本的协议。

<span id="STATUS_LOGIN_WKSTA_RESTRICTION"></span><span id="status_login_wksta_restriction"></span>状态 \_ 登录 \_ WKSTA \_ 限制  
对服务器的工作站登录名存在限制。

以下部分详细介绍了可通过网络小型重定向程序实现的例程：

[内核网络微型重定向程序实现的例程](routines-implemented-by-the-kernel-network-mini-redirector.md)

[RDBSS 未使用的例程](routines-not-used-by-rdbss.md)

基于网络微型重定向程序实现的例程可以根据其功能组织成以下类别：

[连接和名称解析](connection-and-name-resolution.md)

[驱动程序启动、停止和设备控制](driver-start--stop--and-device-control.md)

[文件系统对象创建和删除](file-system-object-creation-and-deletion.md)

[文件系统对象 i/o 例程](file-system-object-i-o-routines.md)

[文件系统对象查询和设置例程](file-system-object-query-and-set-routines.md)

[其他网络小型重定向程序例程](miscellaneous-network-mini-redirector-routines.md)

 

