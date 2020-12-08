---
title: 客户端呈现
description: 客户端呈现
keywords:
- 打印作业 WDK，客户端呈现
- 呈现打印作业 WDK
- 客户端呈现 WDK 打印
- 打印后台处理程序打印-作业渲染 WDK
- 后台处理打印-作业渲染 WDK 打印
- 作业 WDK 打印，客户端呈现
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 36d492c6228b3df3d54214f57a98b8c2d89191ed
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96797717"
---
# <a name="client-side-rendering"></a>客户端呈现


默认情况下，在运行 Windows Vista 的客户端计算机上进行打印作业呈现。

在 Windows 2000 之前，将客户端计算机上呈现的打印作业和呈现的数据发送到打印服务器以进行打印。 自 Windows 2000 和 Windows Vista 之前，打印作业会在打印服务器上进行。 从 Windows 2000 开始，打印作业呈现已移动到打印服务器，这是因为打印服务器比客户端计算机提供的处理能力更多。 更强大的打印服务器可以完成处理大量处理任务的打印作业。

然而，与打印服务器相比，客户端计算机最近的处理器资源通常更多。 此外，许多打印服务器还处理更多的打印队列，同时也充当文件、Web 和邮件服务器。

从 Windows Vista 开始，打印后台处理程序默认在本地呈现打印作业。 打印后台处理程序已更改为启用这种类型的呈现，但打印机驱动程序和最终用户不会注意到任何更改。 大多数打印机驱动程序都不需要进行任何修改即可成功使用客户端呈现;不过，Client-Side 呈现中存在一些 [已知问题](known-issues-with-client-side-rendering.md)中所述的异常。

本节包括：

[客户端呈现概述](client-side-rendering-overview.md)

[客户端呈现的已知问题](known-issues-with-client-side-rendering.md)

[有关客户端呈现的最佳做法](best-practices-for-client-side-rendering.md)

 

 




