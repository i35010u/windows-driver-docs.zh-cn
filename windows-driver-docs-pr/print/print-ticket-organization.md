---
title: 打印票证组织
description: 打印票证组织
keywords:
- 打印入场券 WDK，组织
- 层次结构 WDK 打印票证
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6e0af03a32e3a43fb840e55a82edb01c6358097c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807409"
---
# <a name="print-ticket-organization"></a>打印票证组织


PrintTicket 文档可以包含适用于文档的不同部分的命令。 打印票证文档可以包含以下根据其具体内容分级的内容级别之一：

-   高级别作业 (作业级打印票证) 

-   作业中的文档 (文档级打印票证) 

-   文档中的页面 (页面级别打印票证) 

作业级打印票证最常见，后跟文档级打印票证，最后是最具体的页面级打印票证。 适用于这些级别的 Print Schema Framework 的元素以 "作业"、"文档" 或 "页" 为前缀。 打印票证层次结构与 XPS 文档部件的层次结构相对应。

打印票证的层次结构特性使较低级别打印票证中的元素能够覆盖较高级别的打印票证的对应元素。 在您可以使用 Printticket 之前，必须将它们与文档中较高级别的 PrintTicket 对象合并，应用该文档才能获取特定文档部件的有效打印票证。 此合并在处理所需的有效打印票证之前执行，如打印驱动程序中。

下图显示了不同级别的 PrintTicket 文档和执行此合并的方式之间的关系。

![打印票证层次结构](images/ptpcmerge1.gif)

 

 




