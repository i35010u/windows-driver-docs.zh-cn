---
title: 使用 SignTool 安装目录文件
description: 使用 SignTool 安装目录文件
ms.assetid: b3d151af-d49b-468f-a34a-04e5ab875a07
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe329758b5bb80980a8aa8364199a7be9d704fad
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379459"
---
# <a name="installing-a-catalog-file-by-using-signtool"></a>使用 SignTool 安装目录文件


[**SignTool** ](https://docs.microsoft.com/windows-hardware/drivers/devtest/signtool)不是一个可再发行组件的工具，因此不能是包含重新分发的安装应用程序。 但是，可以在具有 SignTool 符合该工具 Microsoft 软件许可条款的方式已安装的计算机上使用 SignTool。 一个[编录文件](catalog-files.md)可以手动从命令行安装或使用以下 SignTool 命令安装命令脚本：

```cpp
SignTool catdb /v /u CatalogFileName.cat
```

其中：

-   **Catdb**命令配置 SignTool 添加或删除一个目录文件从目录数据库。 默认情况下，SignTool 将目录文件添加到系统组件和驱动程序数据库。

-   **/V**选项配置 SignTool 在详细模式下操作。

-   **/U**选项配置 SignTool 生成要添加的目录文件的唯一名称，如有必要，以阻止替换具有相同的名称的现有目录文件*CatalogFileName.cat*.

-   *CatalogFileName.cat*目录文件的名称。

 

 





