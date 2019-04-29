---
title: 信息泄露
description: 信息泄露
ms.assetid: e5794acb-44f7-4775-854b-69884f60658a
keywords:
- 威胁建模 WDK 文件系统中，信息泄露
- 安全威胁模型 WDK 文件系统中，信息泄露
- 信息泄露 WDK 文件系统
- I/O WDK 的文件系统
- 缓冲区 WDK 文件系统
- 泄露 WDK 的文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c0d0885ff139ee76fc800b28e1dfbbc95bf9ac2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63380957"
---
# <a name="information-disclosure"></a>信息泄露


## <span id="ddk_information_disclosure_if"></span><span id="DDK_INFORMATION_DISCLOSURE_IF"></span>


驱动程序，导致信息泄露通常与公开到不佳缓冲区处理通过应用程序的信息。 例如，使用缓冲 I/O 请求的驱动程序通常指示通过设置所返回的数据量**信息**的成员*IOStatus*阻止结构。 然后，I/O 管理器使用该信息返回到应用程序的缓冲区中复制结果。

如果该驱动程序指示返回更多的数据，I/O 管理器会将来自其他数据复制*SystemBuffer*。 但是，如果该驱动程序未填入的余额*SystemBuffer*，然后的内容相同，内存将返回给应用程序，可能会公开给应用程序的敏感数据。 见证服务器的网络驱动程序的额外信息可能会由于发送到其他系统使用的数据缓冲区未被清除的问题。 例如，ICMP ping 响应可能包含额外信息。 这一问题的无意中公开数据非常真实，并在各种系统中发生。

对于文件系统或文件系统筛选器驱动程序，没有添加了泄漏不应允许访问数据的用户的文件信息的风险。 这可以以多种不同方式完成：

-   使用筛选器驱动程序[ **ZwCreateFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566424)以打开该文件，然后提供对其中间的句柄通过数据的访问。 **Zwcreatefile 转换**函数将默认情况下，打开文件，并绕过安全检查，因为请求来自内核模式。 因此，使用此句柄的访问可能会透露将通常不可用的应用程序的信息。

    如果筛选器驱动程序想要强制执行访问检查，以确保它不公开数据，不应公开，则筛选器驱动程序应指定 OBJ\_FORCE\_访问权限\_签入*ObjectAttributes*的参数[ **ZwCreateFile** ](https://msdn.microsoft.com/library/windows/hardware/ff566424)函数。

-   筛选器驱动程序的打开句柄在内核模式下 （跳过访问检查），但未指定 OBJ\_内核\_处理。 因此创建的句柄被放置在当前进程的句柄表中。 此句柄，具有完全访问权限的数据，然后会显示在用户模式。 恶意应用程序可以监视此类的句柄并尝试使用它们来访问数据。

-   文件系统或文件系统筛选器驱动程序将发布 IRP\_MJ\_创建请求，然后再处理它的系统工作线程上下文中。 系统工作线程处理 IRP 时, 将通常使用系统线程的特权完成创建操作。 因此，使用这些系统特权访问可能会泄露不通常会提供给应用程序的信息。

-   文件系统或文件系统筛选器驱动程序执行基于对象的 I/O 文件而不进行确认调用进程应允许对给定数据的访问。

在中管理和保护信息的唯一角色，由于文件系统和文件系统筛选器驱动程序必须特别警惕中确保其保护的信息。

 

 




