---
title: 异步 I/O 编程
description: 异步 I/O 编程
ms.assetid: f50c98ab-3aae-43f6-be91-2ae587105767
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ac4bd2b94be60cfd5021a5a3e568c4bef4f576c4
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63326059"
---
# <a name="asynchronous-io-programming"></a>异步 I/O 编程


异步编程不会强制其他等待所有人。 这是为编程 Windows 设备驱动程序的首选的技术。 支持异步 I/O 是 WDM 驱动程序的设计目标之一。 有关驱动程序中的异步 I/O 的详细信息，请参阅[支持异步 I/O](supporting-asynchronous-i-o.md)。 设备驱动程序，请使用中断是以异步方式进行编程的最佳方式。 只需将请求发送到你的设备并让系统进行控制。 然后当设备想要说，它将触发中断的操作系统的驱动程序中调用中断处理程序来处理。 此通信是通过 Irp 处理。 有关 IRP 的详细信息，请参阅[处理 Irp](handling-irps.md)。

 

 




