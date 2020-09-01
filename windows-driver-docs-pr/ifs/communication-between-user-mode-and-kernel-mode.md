---
title: 用户模式和内核模式之间的通信
description: 用户模式和内核模式之间的通信
ms.assetid: ddfec0d0-ec7d-4f76-91b8-2cc34cfacf4e
keywords:
- 筛选器管理器 WDK 文件系统微筛选器，通信服务器端口
- 通信服务器端口 WDK 文件系统微筛选器
- 筛选器管理器 WDK 文件系统微筛选器，用户模式/内核模式通信
- 内核模式通信 WDK 文件系统微筛选器
- 用户模式通信 WDK 文件系统微筛选器
- 端口 WDK，文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6aecaae3400b0a2f011f0e8243a0c84d9f3fed77
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89065334"
---
# <a name="communication-between-user-mode-and-kernel-mode"></a>用户模式和内核模式之间的通信


筛选器管理器通过通信端口支持用户模式和内核模式间的通信。 微筛选器驱动程序通过指定要应用于通信端口对象的安全描述符来控制端口上的安全性。 通过通信端口的通信不会进行缓冲，因此它的速度更快，效率更高。 用户模式的应用程序或服务可以回复来自微筛选器驱动程序的消息以进行双向通信。

当微筛选器驱动程序创建通信服务器端口时，它会隐式开始侦听端口上的传入连接。 当用户模式调用方尝试连接到端口时，筛选器管理器将使用新创建的连接的句柄调用微筛选器驱动程序的 [**ConnectNotifyCallback**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatecommunicationport) 例程。 当筛选器管理器重新获得控制时，它将向用户模式调用方传递一个单独的文件句柄，该句柄表示到连接的用户模式调用方的终结点。 此句柄可用于将 i/o 完成端口与侦听器端口关联。

仅当用户模式调用方具有端口上的安全描述符指定的足够访问权限时，才接受连接。 端口的每个连接都将获取其自己的消息队列和专用终结点。

关闭任一终结点 (内核或用户) 终止该连接。 当用户模式调用方关闭其对终结点的句柄时，筛选器管理器将调用微筛选器驱动程序的 [**DisconnectNotifyCallback**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatecommunicationport) 例程，使微筛选器驱动程序可以关闭其连接的句柄。

关闭通信服务器端口会阻止新连接，但不会终止现有连接。 筛选器管理器将在卸载微筛选器驱动程序时终止现有连接。

### <a name="span-idfilter_manager_routines_for_communication_between_user_mode_and_kernel_modespanspan-idfilter_manager_routines_for_communication_between_user_mode_and_kernel_modespanspan-idfilter_manager_routines_for_communication_between_user_mode_and_kernel_modespanfilter-manager-routines-for-communication-between-user-mode-and-kernel-mode"></a><span id="Filter_Manager_Routines_for_Communication_Between_User_Mode_and_Kernel_Mode"></span><span id="filter_manager_routines_for_communication_between_user_mode_and_kernel_mode"></span><span id="FILTER_MANAGER_ROUTINES_FOR_COMMUNICATION_BETWEEN_USER_MODE_AND_KERNEL_MODE"></span>用于在用户模式和内核模式之间进行通信的筛选器管理器例程

筛选器管理器为内核模式微筛选器驱动程序提供以下支持例程，以与用户模式应用程序进行通信：

[**FltCloseClientPort**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcloseclientport)

[**FltCloseCommunicationPort**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltclosecommunicationport)

[**FltCreateCommunicationPort**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatecommunicationport)

[**FltSendMessage**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltsendmessage)

为用户模式应用程序提供了以下支持例程来与微筛选器驱动程序通信：

[**FilterConnectCommunicationPort**](/windows/desktop/api/fltuser/nf-fltuser-filterconnectcommunicationport)

[**FilterGetMessage**](/windows/desktop/api/fltuser/nf-fltuser-filtergetmessage)

[**FilterReplyMessage**](/windows/desktop/api/fltuser/nf-fltuser-filterreplymessage)

[**FilterSendMessage**](/windows/desktop/api/fltuser/nf-fltuser-filtersendmessage)

### <a name="span-idminifilter_driver_callback_routines_for_communication_between_user_mode_and_kernel_modespanspan-idminifilter_driver_callback_routines_for_communication_between_user_mode_and_kernel_modespanspan-idminifilter_driver_callback_routines_for_communication_between_user_mode_and_kernel_modespanminifilter-driver-callback-routines-for-communication-between-user-mode-and-kernel-mode"></a><span id="Minifilter_Driver_Callback_Routines_for_Communication_Between_User_Mode_and_Kernel_Mode"></span><span id="minifilter_driver_callback_routines_for_communication_between_user_mode_and_kernel_mode"></span><span id="MINIFILTER_DRIVER_CALLBACK_ROUTINES_FOR_COMMUNICATION_BETWEEN_USER_MODE_AND_KERNEL_MODE"></span>用于在用户模式和内核模式之间进行通信的微筛选器驱动程序回调例程

以下微筛选器驱动程序回调例程作为参数传递给 [**FltCreateCommunicationPort**](/windows-hardware/drivers/ddi/fltkernel/nf-fltkernel-fltcreatecommunicationport)：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">回调例程名称</th>
<th align="left">回调例程类型</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><em>ConnectNotifyCallback</em></p></td>
<td align="left"><p>PFLT_CONNECT_NOTIFY</p></td>
</tr>
<tr class="even">
<td align="left"><p><em>DisconnectNotifyCallback</em></p></td>
<td align="left"><p>PFLT_DISCONNECT_NOTIFY</p></td>
</tr>
<tr class="odd">
<td align="left"><p><em>MessageNotifyCallback</em></p></td>
<td align="left"><p>PFLT_MESSAGE_NOTIFY</p></td>
</tr>
</tbody>
</table>

 

 

