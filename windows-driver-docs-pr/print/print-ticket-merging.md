---
title: 打印票证合并
description: 打印票证合并
ms.assetid: 2d9cf4d3-5c73-4355-b5e0-effcfb7102cc
keywords:
- XPSDrv 的打印机驱动程序 WDK，呈现模块
- 呈现模块 WDK XPSDrv 打印票证
- 打印票证 WDK，XPSDrv 的打印机驱动程序
- 合并的打印票证对象
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3e49acda9d9b06ac9a237061812545716df3e1f6
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542102"
---
# <a name="print-ticket-merging"></a>打印票证合并


在打印驱动程序中处理的 PrintTicket 对象具有层次结构关系基于与之关联的文档部分。 下图说明了 XPS 文档中的这些部分的关系。

![说明在 xps 文档中的文档部件的关系图](images/ptpcxps1.gif)

每个层次结构中的打印票证级别有不同的作用域。 使用的打印票证信息的打印驱动程序筛选器模块必须维护该作用域作为从文档流中读取对象打印票证。 下图说明了如何进行这种打印驱动程序筛选器模块中。

![说明如何不同打印票证级别的关系图以逻辑方式合并 ](images/ptpcxps2.gif)

当筛选器中读取文档部件时，打印票证对象是读取、 合并和验证和缓存配置筛选器将如何处理每个文档部件的筛选器。 上面的关系图说明了如何以逻辑方式合并不同的打印票证级别和下面的伪代码说明了这一合并可能会实现方式。

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

 

 




