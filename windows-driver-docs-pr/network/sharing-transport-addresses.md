---
title: 共享传输地址
description: 共享传输地址
keywords:
- 共享传输地址
- 绑定套接字 WDK Winsock 内核
- 本地传输地址绑定 WDK Winsock 内核
- 传输地址 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 8d1a80021a0baa82fe55641ffa35fb18f1c1c912
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96837911"
---
# <a name="sharing-transport-addresses"></a>共享传输地址


在大多数情况下，Winsock 内核 (WSK) 应用程序无法将套接字绑定到已由另一套接字使用的本地传输地址。 WSK 应用程序可使用 [ \_ EXCLUSIVEADDRUSE](./so-exclusiveaddruse.md) 等 [ \_ REUSEADDR](./so-reuseaddr.md) 套接字选项控制套接字绑定到的本地传输地址的共享。 默认情况下，不会为套接字设置这两个套接字选项。 有关设置套接字选项的详细信息，请参阅 [在套接字上执行控制操作](performing-control-operations-on-a-socket.md)。

下表显示了将另一套接字绑定到已由另一套接字使用的本地传输地址的结果。 *通配符* 和 *特定* 情况指定套接字绑定到通配符本地传输地址，还是绑定到特定的本地传输地址。

 <table>
     <tr>
      <th colspan="2" rowspan="3">第二次绑定</th>
      <th colspan="6">第一次绑定</th>
     </tr>
     <tr>
      <td colspan="2">
       <p> (默认) 无套接字选项
       </p>
      </td>
      <td colspan="2">
       <p>
        SO_REUSEADDR
       </p>
      </td>
      <td colspan="2">
       <p>
        SO_EXCLUSIVEADDRUSE
       </p>
      </td>
     </tr>
     <tr>
      <td>
       <p>
        通配符
       </p>
      </td>
      <td>
       <p>
        特定
       </p>
      </td>
      <td>
       <p>
        通配符
       </p>
      </td>
      <td>
       <p>
        特定
       </p>
      </td>
      <td>
       <p>
        通配符
       </p>
      </td>
      <td>
       <p>
        特定
       </p>
      </td>
     </tr>
     <tr>
      <td rowspan="2">
       <p>
         (默认) 无套接字选项
       </p>
      </td>
      <td>
       <p>
        通配符
       </p>
      </td>
      <td>
       <p>正在使用</p>
      </td>
      <td>
       <p>成功</p>
      </td>
      <td>
       <p>正在使用</p>
      </td>
      <td>
       <p>成功</p>
      </td>
      <td>
       <p>正在使用</p>
      </td>
      <td>
       <p>成功</p>
      </td>
     </tr>
     <tr>
      <td>
       <p>
        特定
       </p>
      </td>
      <td>
       <p>CHECK</p>
      </td>
      <td>
       <p>正在使用</p>
      </td>
      <td>
       <p>CHECK</p>
      </td>
      <td>
       <p>拒绝</p>
      </td>
      <td>
       <p>拒绝</p>
      </td>
      <td>
       <p>正在使用</p>
      </td>
     </tr>
     <tr>
      <td rowspan="2">
       <p>
        SO_REUSEADDR
       </p>
      </td>
      <td>
       <p>
        通配符
       </p>
      </td>
      <td>
       <p>拒绝</p>
      </td>
      <td>
       <p>成功</p>
      </td>
      <td>
       <p>成功</p>
      </td>
      <td>
       <p>成功</p>
      </td>
      <td>
       <p>拒绝</p>
      </td>
      <td>
       <p>成功</p>
      </td>
     </tr>
     <tr>
      <td>
       <p>
        特定
       </p>
      </td>
      <td>
       <p>CHECK</p>
      </td>
      <td>
       <p>拒绝</p>
      </td>
      <td>
       <p>成功</p>
      </td>
      <td>
       <p>成功</p>
      </td>
      <td>
       <p>拒绝</p>
      </td>
      <td>
       <p>拒绝</p>
      </td>
     </tr>
     <tr>
      <td rowspan="2">
       <p>
        SO_EXCLUSIVEADDRUSE
       </p>
      </td>
      <td>
       <p>
        通配符
       </p>
      </td>
      <td>
       <p>正在使用</p>
      </td>
      <td>
       <p>正在使用</p>
      </td>
      <td>
       <p>正在使用</p>
      </td>
      <td>
       <p>正在使用</p>
      </td>
      <td>
       <p>正在使用</p>
      </td>
      <td>
       <p>正在使用</p>
      </td>
     </tr>
     <tr>
      <td>
       <p>
        特定
       </p>
      </td>
      <td>
       <p>CHECK</p>
      </td>
      <td>
       <p>正在使用</p>
      </td>
      <td>
       <p>CHECK</p>
      </td>
      <td>
       <p>正在使用</p>
      </td>
       <td>
       <p>拒绝</p>
      </td>
      <td>
       <p>正在使用</p>
      </td>
     </tr>
    </table>    

结果定义如下：

<a href="" id="success"></a>辉煌  
第二个套接字的绑定操作成功。 WSK 子系统返回状态为 "成功" 的状态 \_ 。

<a href="" id="inuse"></a>正在使用  
对第二个套接字的绑定操作失败。 WSK 子系统返回状态 \_ 地址已存在的状态 \_ \_ 。

<a href="" id="denied"></a>拒绝  
对第二个套接字的绑定操作失败。 WSK 子系统返回状态 " \_ 访问被拒绝" 的状态 \_ 。

<a href="" id="check"></a>查阅  
执行访问检查来确定第二个套接字上的绑定操作是成功还是失败。 如果授予访问权限，则绑定成功，且 WSK 子系统返回状态为 "成功" 的状态 \_ 。 如果访问被拒绝，则绑定将失败，并且 WSK 子系统返回状态 " \_ 访问被拒绝" 的状态 \_ 。

在上表中定义了执行访问检查的情况下，将根据第一个套接字的安全描述符来检查第二个套接字的安全上下文。

-   套接字的安全上下文由在创建套接字时传递到 [WskSocket](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket)函数或 [WskSocketConnect](/windows-hardware/drivers/ddi/wsk/nc-wsk-pfn_wsk_socket_connect)函数的 *OwningProcess* 和 *OwningThread* 参数决定。 如果在创建套接字时未指定任何特定进程或线程，则使用创建套接字的进程的安全上下文。

-   套接字的安全描述符由传递到 WskSocket 函数的 *SecurityDescriptor* 参数或在创建套接字时的 WskSocketConnect 函数指定。 如果未指定特定的安全描述符，WSK 子系统将使用不允许共享传输地址的默认安全描述符。 使用 [ \_ WSK \_ security](./so-wsk-security.md) socket 选项创建套接字后，还可以将安全描述符应用到套接字。

如果两个套接字绑定到两个不同的特定本地传输地址，则这两个传输地址均不共享。 在这种情况下，第二个绑定操作始终会成功完成。

 

