---
title: 自动配置 GPD 的打印机内存
description: 自动配置 GPD 的打印机内存
ms.assetid: 5e8339a5-d515-4821-853e-bc6607b2d9c1
keywords:
- 内存 WDK 打印机自动配置
- GPD 文件 WDK GDL 扩展，内存
- 框中自动配置支持 WDK 打印机，内存
- autoconfiguring 打印机内存 WDK
- 打印机内存配置 WDK 自动配置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ece6688e56a9f3e601ff76272c83383268b1d313
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349275"
---
# <a name="autoconfiguring-the-printers-memory-for-gpd"></a>自动配置 GPD 的打印机内存


下面的代码示例演示如何将条目添加到 GPD 文件中的任何内存选项 GDL 文件。 下面的示例后显示 GPD 代码示例是典型的内存功能的定义。

```GPD
*Feature: Memory
{
  *rcNameID: =PRINTER_MEMORY_DISPLAY
  *DefaultOption: 4096KB

  *MemConfigKB: PAIR(4096, 3150)
  *MemConfigKB: PAIR(8192, 6750)
}
```

可以通过将以下功能添加到 GDL 文件启用内存自动配置。

```GDL
*% This feature definition merges with the definition in the GPD file
*Feature: Memory
{
  *% *BidiQuery and *BidiResponse constructs must have the same names
  *BidiQuery: Memory
  {
  *QueryString: "\Printer.Configuration.Memory:Size"
  }
  *BidiResponse: Memory
   {
    *ResponseType: BIDI_INT
    *ResponseData: ENUM_OPTION (Memory)
  }

  *Option: 4096KB
  {
    *% Names for the memory options already defined in GPD
    *BidiValue: INT(4096)
  }

  *Option: 8192KB
  {
    *BidiValue: INT(8192)
  }
}
```








