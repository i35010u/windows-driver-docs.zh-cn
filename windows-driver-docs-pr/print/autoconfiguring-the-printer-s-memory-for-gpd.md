---
title: 自动配置 GPD 的打印机内存
description: 自动配置 GPD 的打印机内存
keywords:
- 内存 WDK 打印机自动配置
- GPD 文件 WDK GDL 扩展，内存
- 内置自动配置支持 WDK 打印机，内存
- autoconfiguring 打印机内存 WDK
- 打印机内存配置 WDK 自动配置
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 721cdf7074b2730c95ba146b5718c5d0dbda4f60
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836079"
---
# <a name="autoconfiguring-the-printers-memory-for-gpd"></a>自动配置 GPD 的打印机内存


下面的代码示例演示了如何在 GDL 文件中为 GPD 文件中的任何内存选项添加项。 下面的示例中显示的 GPD 代码示例是内存功能的典型定义。

```GPD
*Feature: Memory
{
  *rcNameID: =PRINTER_MEMORY_DISPLAY
  *DefaultOption: 4096KB

  *MemConfigKB: PAIR(4096, 3150)
  *MemConfigKB: PAIR(8192, 6750)
}
```

可以通过将以下功能添加到 GDL 文件来启用内存自动配置。

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








