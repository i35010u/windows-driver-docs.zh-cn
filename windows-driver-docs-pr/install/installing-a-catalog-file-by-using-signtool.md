---
title: 使用 SignTool 安装目录文件
description: 使用 SignTool 安装目录文件
ms.assetid: b3d151af-d49b-468f-a34a-04e5ab875a07
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3eb7e93bf1855b38faa7bc4f26105ca1fe7ae916
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097293"
---
# <a name="installing-a-catalog-file-by-using-signtool"></a>使用 SignTool 安装目录文件


[**SignTool**](../devtest/signtool.md) 不是可再发行的工具，因此无法包括在重新分发的安装应用程序中。 但是，可以在安装了 SignTool 的计算机上使用 SignTool，该计算机符合该工具的 Microsoft 软件许可条款。 [目录文件](catalog-files.md)可以从命令行手动安装，也可以通过命令脚本使用以下 SignTool 命令进行安装：

```cpp
SignTool catdb /v /u CatalogFileName.cat
```

其中：

-   **Catdb**命令将 SignTool 配置为在目录数据库中添加或删除编录文件。 默认情况下，SignTool 会将目录文件添加到系统组件和驱动程序数据库。

-   **/V**选项将 SignTool 配置为在详细模式下运行。

-   **/U**选项将 SignTool 配置为为正在添加的目录文件生成唯一名称（如有必要）以防止替换现有的同名目录文件，该文件具有与*CatalogFileName.cat*相同的名称。

-   *CatalogFileName.cat* 是目录文件的名称。

 

