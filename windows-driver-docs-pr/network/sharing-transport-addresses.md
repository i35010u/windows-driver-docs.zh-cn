---
title: 共享传输地址
description: 共享传输地址
ms.assetid: 1f5bc91a-75eb-466c-ad7d-cfbe0e83dc17
keywords:
- 共享传输地址
- 绑定套接字 WDK Winsock 内核
- 本地传输地址绑定 WDK Winsock 内核
- 传输地址 WDK Winsock 内核
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fd4d6fd1cc3f110e6694616c7196bc4a123f5c6e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362012"
---
# <a name="sharing-transport-addresses"></a>共享传输地址


在大多数情况下，Winsock Kernel (WSK) 应用程序不能将套接字绑定到已在另一套接字使用的本地传输地址。 WSK 应用程序可以使用[因此\_EXCLUSIVEADDRUSE](https://msdn.microsoft.com/library/windows/hardware/ff570830)并[因此\_REUSEADDR](https://msdn.microsoft.com/library/windows/hardware/ff570833)套接字绑定到套接字选项来控制共享本地传输地址。 默认情况下，这两个套接字选项都设置为套接字。 设置套接字选项的详细信息，请参阅[套接字上执行管理操作](performing-control-operations-on-a-socket.md)。

下表显示了第二个套接字绑定到已在另一套接字使用的本地传输地址的结果。 *通配符*并*特定*情况下指定套接字绑定到通配符本地传输地址或特定的本地传输地址。

 <table>
     <tr>
      <th colspan="2" rowspan="3">第二个绑定</th>
      <th colspan="6">第一次绑定</th>
     </tr>
     <tr>
      <td colspan="2">
       <p>没有套接字选项 （默认值）
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
        指定的
       </p>
      </td>
      <td>
       <p>
        通配符
       </p>
      </td>
      <td>
       <p>
        指定的
       </p>
      </td>
      <td>
       <p>
        通配符
       </p>
      </td>
      <td>
       <p>
        指定的
       </p>
      </td>
     </tr>
     <tr>
      <td rowspan="2">
       <p>
        没有套接字选项 （默认值）
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
        指定的
       </p>
      </td>
      <td>
       <p>检查</p>
      </td>
      <td>
       <p>正在使用</p>
      </td>
      <td>
       <p>检查</p>
      </td>
      <td>
       <p>被拒绝</p>
      </td>
      <td>
       <p>被拒绝</p>
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
       <p>被拒绝</p>
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
       <p>被拒绝</p>
      </td>
      <td>
       <p>成功</p>
      </td>
     </tr>
     <tr>
      <td>
       <p>
        指定的
       </p>
      </td>
      <td>
       <p>检查</p>
      </td>
      <td>
       <p>被拒绝</p>
      </td>
      <td>
       <p>成功</p>
      </td>
      <td>
       <p>成功</p>
      </td>
      <td>
       <p>被拒绝</p>
      </td>
      <td>
       <p>被拒绝</p>
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
        指定的
       </p>
      </td>
      <td>
       <p>检查</p>
      </td>
      <td>
       <p>正在使用</p>
      </td>
      <td>
       <p>检查</p>
      </td>
      <td>
       <p>正在使用</p>
      </td>
       <td>
       <p>被拒绝</p>
      </td>
      <td>
       <p>正在使用</p>
      </td>
     </tr>
    </table>    

结果定义，如下所示：

<a href="" id="success"></a>成功  
第二个套接字绑定操作会成功。 WSK 子系统返回的状态\_成功。

<a href="" id="inuse"></a>正在使用  
第二个套接字上的绑定操作将失败。 WSK 子系统返回的状态\_地址\_ALREADY\_EXISTS。

<a href="" id="denied"></a>被拒绝  
第二个套接字上的绑定操作将失败。 WSK 子系统返回的状态\_访问\_被拒绝。

<a href="" id="check"></a>检查  
执行访问检查，确定第二个套接字上的绑定操作是成功还是失败。 如果授予访问权限，绑定成功并且 WSK 子系统返回的状态\_成功。 如果访问被拒绝，绑定将失败，WSK 子系统返回的状态\_访问\_被拒绝。

在其中执行访问检查上一个表中定义的情况下，将针对第一个套接字的安全描述符检查第二个套接字的安全上下文。

-   套接字的安全上下文由*OwningProcess*并*OwningThread*传递的参数为[WskSocket](https://msdn.microsoft.com/library/windows/hardware/ff571149)函数或[WskSocketConnect](https://msdn.microsoft.com/library/windows/hardware/ff571150)函数时创建套接字。 如果没有特定的进程或线程指定创建套接字时，，使用创建套接字的进程的安全上下文。

-   指定套接字的安全描述符*SecurityDescriptor*创建套接字时传递给 WskSocket 函数或 WskSocketConnect 函数的参数。 如果未不指定任何特定的安全描述符，WSK 子系统将使用不允许使用共享的传输地址的默认安全描述符。 安全描述符可以还可应用于一个套接字后通过使用而创建的套接字[因此\_WSK\_安全](https://msdn.microsoft.com/library/windows/hardware/ff570835)套接字选项。

如果两个套接字绑定到两个不同的特定本地传输地址，不会发生共享的传输地址。 在此情况下的第二个绑定操作将始终成功完成。

 

 





