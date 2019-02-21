---
title: 用户模式和内核模式之间的通信
description: 用户模式和内核模式之间的通信
ms.assetid: ddfec0d0-ec7d-4f76-91b8-2cc34cfacf4e
keywords:
- 筛选器管理器 WDK 文件系统微筛选器，通信服务器端口
- 通信服务器端口 WDK 文件系统微筛选器
- 筛选器管理器 WDK 文件系统微筛选器，用户模式/内核模式下通信
- 内核模式下通信 WDK 文件系统微筛选器
- 用户模式下通信 WDK 文件系统微筛选器
- 端口 WDK，文件系统微筛选器
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a39f91c6f69747f6169b0daa13ea4b72ab4363a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519297"
---
# <a name="communication-between-user-mode-and-kernel-mode"></a>用户模式和内核模式之间的通信


筛选器管理器支持用户模式和内核模式下通过通信端口之间的通信。 微筛选器驱动程序通过指定要应用于通信端口对象的安全描述符控制的端口上的安全。 通过通信端口的通信是不会缓冲，因此，更快、 更高效。 用户模式应用程序或服务可以回复消息从微筛选器驱动程序来进行双向通信。

当微筛选器驱动程序创建通信服务器端口时，它隐式开始侦听的端口上的传入连接。 当用户模式下调用方尝试连接到的端口时，筛选器管理器调用微筛选器驱动程序[ **ConnectNotifyCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff541931)例程替换为新创建的连接的句柄。 当筛选器管理器重新获得控制时，它会将用户模式下调用方传递一个表示连接的用户模式下调用方的终结点的单独的文件句柄。 可以使用此句柄将 I/O 完成端口侦听器端口与相关联。

仅当用户模式下调用方具有足够的访问权限的安全描述符由指定的端口上接受连接。 每次连接到端口获取其自己的消息队列和专用终结点。

关闭其中任一终结点 （内核或用户） 将终止该连接。 当用户模式下调用方关闭其句柄到终结点时，筛选器管理器调用微筛选器驱动程序[ **DisconnectNotifyCallback** ](https://msdn.microsoft.com/library/windows/hardware/ff541931)例程，因此微筛选器驱动程序可以关闭其句柄连接。

关闭通信服务器端口可防止新连接，但并不终止现有连接。 卸载微筛选器驱动程序时，筛选器管理器会终止现有连接。

### <a name="span-idfiltermanagerroutinesforcommunicationbetweenusermodeandkernelmodespanspan-idfiltermanagerroutinesforcommunicationbetweenusermodeandkernelmodespanspan-idfiltermanagerroutinesforcommunicationbetweenusermodeandkernelmodespanfilter-manager-routines-for-communication-between-user-mode-and-kernel-mode"></a><span id="Filter_Manager_Routines_for_Communication_Between_User_Mode_and_Kernel_Mode"></span><span id="filter_manager_routines_for_communication_between_user_mode_and_kernel_mode"></span><span id="FILTER_MANAGER_ROUTINES_FOR_COMMUNICATION_BETWEEN_USER_MODE_AND_KERNEL_MODE"></span>用户模式和内核模式之间进行通信的筛选器管理器例程

筛选器管理器提供了以下支持例程适用于内核模式微筛选器驱动程序与用户模式应用程序进行通信：

[**FltCloseClientPort**](https://msdn.microsoft.com/library/windows/hardware/ff541867)

[**FltCloseCommunicationPort**](https://msdn.microsoft.com/library/windows/hardware/ff541871)

[**FltCreateCommunicationPort**](https://msdn.microsoft.com/library/windows/hardware/ff541931)

[**FltSendMessage**](https://msdn.microsoft.com/library/windows/hardware/ff544378)

为用户模式应用程序与微筛选器驱动程序进行通信提供了以下支持例程：

[**FilterConnectCommunicationPort**](https://msdn.microsoft.com/library/windows/hardware/ff540460)

[**FilterGetMessage**](https://msdn.microsoft.com/library/windows/hardware/ff540506)

[**FilterReplyMessage**](https://msdn.microsoft.com/library/windows/hardware/ff541508)

[**FilterSendMessage**](https://msdn.microsoft.com/library/windows/hardware/ff541513)

### <a name="span-idminifilterdrivercallbackroutinesforcommunicationbetweenusermodeandkernelmodespanspan-idminifilterdrivercallbackroutinesforcommunicationbetweenusermodeandkernelmodespanspan-idminifilterdrivercallbackroutinesforcommunicationbetweenusermodeandkernelmodespanminifilter-driver-callback-routines-for-communication-between-user-mode-and-kernel-mode"></a><span id="Minifilter_Driver_Callback_Routines_for_Communication_Between_User_Mode_and_Kernel_Mode"></span><span id="minifilter_driver_callback_routines_for_communication_between_user_mode_and_kernel_mode"></span><span id="MINIFILTER_DRIVER_CALLBACK_ROUTINES_FOR_COMMUNICATION_BETWEEN_USER_MODE_AND_KERNEL_MODE"></span>用户模式和内核模式之间进行通信的微筛选器驱动程序回调例程

下面的微筛选器驱动程序回调例程作为参数传递到[ **FltCreateCommunicationPort**](https://msdn.microsoft.com/library/windows/hardware/ff541931):

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

 

 

 




