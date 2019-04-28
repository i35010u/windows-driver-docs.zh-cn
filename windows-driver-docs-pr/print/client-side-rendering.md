---
title: 客户端呈现
description: 客户端呈现
ms.assetid: 7b67de2a-b5aa-4d8c-9b2c-9caeffdb71c3
keywords:
- 打印作业 WDK，客户端呈现
- 呈现打印作业 WDK
- 客户端呈现 WDK 打印
- 打印后台处理程序的打印作业呈现 WDK
- 打印后台处理程序的打印作业呈现 WDK
- 作业 WDK 打印、 客户端的呈现方式
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bef7c62d7324045175bedc008f44046a682f3d60
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351949"
---
# <a name="client-side-rendering"></a>客户端呈现


打印作业呈现发生，默认情况下，运行的 Windows Vista 的客户端计算机上。

Windows 2000 之前 Windows 呈现客户端计算机上的打印作业并呈现的数据发送到打印服务器进行打印。 自 Windows 2000 和 Windows Vista 之前，打印作业呈现发生在打印服务器上。 打印作业呈现已将移到打印服务器从 Windows 2000 开始，原因是打印服务器提供了更多处理能力比客户端计算机。 然后，功能更强大的打印服务器无法完成的打印作业呈现大量占用处理器的任务。

最近，但是，客户端计算机通常具有更多可用的处理器资源比打印服务器。 此外，许多打印服务器处理多个打印队列和也用作文件、 Web 和邮件服务器。

从 Windows Vista 开始，打印后台处理程序呈现打印作业本地默认情况下。 打印后台处理程序已更改，以启用这种类型的呈现，但打印机驱动程序和最终用户将看不到任何更改。 大多数打印机驱动程序不需要任何修改为使用客户端成功，则呈现但是，有一些例外情况中所述[与客户端呈现的已知问题](known-issues-with-client-side-rendering.md)。

本部分包括：

[客户端呈现概述](client-side-rendering-overview.md)

[客户端呈现的已知的问题](known-issues-with-client-side-rendering.md)

[客户端呈现的最佳做法](best-practices-for-client-side-rendering.md)

 

 




