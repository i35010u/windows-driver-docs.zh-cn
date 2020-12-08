---
title: 打印票证合并
description: 打印票证合并
keywords:
- XPSDrv 打印机驱动程序 WDK，呈现模块
- 渲染模块 WDK XPSDrv，打印票证
- 打印票证 WDK，XPSDrv 打印机驱动程序
- 合并打印票证对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c3ef8be586ab021b7668e12aeaf215f38523e187
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96807411"
---
# <a name="print-ticket-merging"></a>打印票证合并


打印驱动程序中处理的 PrintTicket 对象具有基于其关联的文档部件的层次结构关系。 下图说明了这些部件在 XPS 文档中的关系。

![阐释 xps 文档中文档部件的关系图](images/ptpcxps1.gif)

层次结构中的每个打印票证级别都有不同的范围。 使用打印票证信息的打印驱动程序筛选器模块必须维护该范围，因为打印票证对象是从文档流中读取的。 下图说明了如何在打印驱动程序筛选器模块中完成此操作。

![说明如何以逻辑方式合并不同打印票证级别的关系图 ](images/ptpcxps2.gif)

当筛选器读取文档部件时，筛选器将读取、合并和验证打印票证对象并缓存这些对象，以配置筛选器处理每个文档部件的方式。 上图说明了如何对不同的打印票证级别进行逻辑合并，下面的伪代码演示了如何实现此合并。

```cpp
class Filter
{
 PrintTicket Saved_FDS_PT;
 PrintTicket Saved_FD_PT;

 ProcessFDS(pIFixedDocumentSequence)
    {
 Saved_FDS_PT = pIFixedDocumentSequence->GetPrintTicket();

        // continue processing the FixedDocumentSequence part
    }

 ProcessFD(pIFixedDocument)
    {
 Saved_FD_PT->Release();

        temp = pIFixedDocument->GetPrintTicket();

 Saved_FD_PT = PrintTicketMergeAndValidate(
 Saved_FDS_PT, temp);

        // continue processing the FixedDocument part
    }

 ProcessPage(IFixedPage)
    {
        temp = pIFixedPage->GetPrintTicket();

 PagePT = PrintTicketMergeAndValidate(Saved_FD_PT, temp);

        // continue processing the FixedPage part
    }

 PrintTicket PrintTicketMergeAndValidate(
 ParentPT,
 PartPT)
    {
        // Entries in the Part PrintTicket 
        // take precedence over the corresponding entries 
        // in the Parent PrintTicket
    }
};
```

 

 




