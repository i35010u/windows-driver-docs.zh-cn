---
title: 打印票证组织
description: 打印票证组织
ms.assetid: 3e30eb53-2f62-469d-a27c-dc256df37126
keywords:
- 打印票证 WDK，组织
- 层次结构 WDK 打印票证
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 68b09ffbce4403a74450f5a276bfe8e638c4c9d6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63351904"
---
# <a name="print-ticket-organization"></a>打印票证组织


PrintTicket 文档可以包含应用于文档的不同部分的命令。 打印票证文档可以包含以下按照其特异性排序的内容级别之一：

-   高级作业 （职位等级打印票证）

-   作业 （文档级打印票证） 中的文档

-   文档 （页面级别打印票证） 中的页

作业级打印票证是最常见的后, 跟文档级别打印票证，并最后页面级别打印票证，这是最具体的。 适用于这些级别的打印架构框架元素前缀为"作业"、"文档"或"Page"相应地。 打印票证层次结构对应于 XPS 文档部件的层次结构。

打印票证的层次结构性质使较低级别的打印票证，以重写的更高级别的打印票证的相应元素中的元素。 可以使用 Printticket 之前，它们必须与应用以获取有效的特定文档部件的打印票证的更高级别文档中的 PrintTicket 对象合并。 处理命令，例如打印驱动程序需要提供有效的打印票证之前，会执行此合并。

下图显示在不同级别的 PrintTicket 文档和如何执行此合并之间的关系。

![打印票证层次结构](images/ptpcmerge1.gif)

 

 




