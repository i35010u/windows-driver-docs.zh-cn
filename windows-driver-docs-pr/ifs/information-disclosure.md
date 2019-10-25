---
title: 信息泄露
description: 信息泄露
ms.assetid: e5794acb-44f7-4775-854b-69884f60658a
keywords:
- 系统威胁模型 WDK 文件系统，信息泄露
- 安全威胁模型 WDK 文件系统，信息泄露
- 信息泄露 WDK 文件系统
- I/o WDK 文件系统
- 缓冲 WDK 文件系统
- 泄露 WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cd43d2ec3c212cfb4adb656735e8bcd4fd9e072a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841202"
---
# <a name="information-disclosure"></a>信息泄露


## <span id="ddk_information_disclosure_if"></span><span id="DDK_INFORMATION_DISCLOSURE_IF"></span>


对于驱动程序，信息泄露通常涉及到通过不良缓冲区处理向应用程序公开信息。 例如，具有缓冲 i/o 请求的驱动程序通常通过设置*IOStatus*块结构的**信息**成员，指示要返回的数据量。 然后，i/o 管理器使用该信息将结果复制回应用程序的缓冲区。

如果驱动程序指示返回的数据越多，i/o 管理器将从*SystemBuffer*复制其他数据。 但是，如果驱动程序未填充*SystemBuffer*，则该内存中的任何内容都将返回到应用程序，这可能会向应用程序公开敏感数据。 见证网络驱动程序的问题，其中可能会向其他系统发送额外信息，因为未清除使用的数据缓冲区。 例如，ICMP ping 响应可能包含附加信息。 无意间公开数据的这一问题非常真实，并发生在各种系统中。

对于文件系统或文件系统筛选器驱动程序，增加了向不允许访问数据的用户泄露文件信息的风险。 可以通过多种不同的方式实现此目的：

-   使用[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)打开文件的筛选器驱动程序，然后通过其中间句柄提供对数据的访问。 默认情况下， **ZwCreateFile**函数将打开文件并绕过安全检查，因为请求来自内核模式。 因此，使用此句柄的访问可能会泄露通常不适用于应用程序的信息。

    如果筛选器驱动程序希望强制执行访问检查以确保它不会公开不应公开的数据，则筛选器驱动程序应指定 OBJ\_强制\_访问，\_签入[**ZwCreateFile**](https://docs.microsoft.com/windows-hardware/drivers/ddi/ntifs/nf-ntifs-ntcreatefile)函数。

-   一种筛选器驱动程序，用于打开内核模式下的句柄（绕过访问检查），但未指定\_内核\_句柄的 OBJ。 因此，创建的句柄会置于当前进程的句柄表中。 此句柄具有对数据的完全访问权限，然后在用户模式下可见。 恶意应用程序可能会监视此类句柄，并尝试使用它们来访问数据。

-   文件系统或文件系统筛选器驱动程序，它将 IRP\_MJ 发送\_创建请求，然后在系统工作线程的上下文中对其进行处理。 当系统工作线程处理 IRP 时，通常使用系统线程的权限来完成创建操作。 因此，使用这些系统权限的访问可能会泄露通常不能用于应用程序的信息。

-   一种文件系统或文件系统筛选器驱动程序，它执行基于文件对象的 i/o，而不确认是否允许调用进程访问给定数据。

由于文件系统和文件系统筛选器驱动程序在管理和保护信息方面具有独特的作用，因此必须特别小心地确保其保护信息。

 

 




