---
title: 将 GDL 扩展添加到现有的 GPD 文件
description: 将 GDL 扩展添加到现有的 GPD 文件
keywords:
- 内置自动配置支持 WDK 打印机，GDL 扩展
- GDL 文件 WDK 打印机
- 扩展 WDK GDL 文件
- GPD 文件 WDK GDL 扩展
- GPD 文件 WDK GDL 扩展，添加
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: de592f7d4bf360e87a78c9bac4fd8ea37bc6a2f5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96812413"
---
# <a name="adding-gdl-extensions-to-an-existing-gpd-file"></a>将 GDL 扩展添加到现有的 GPD 文件


如果要将自动配置的支持添加到现有的 GPD 文件，应执行以下操作：

1.  创建 GDL 文件。 GDL 文件应具有与 **\* 功能** 选项构造对应的 **\* BidiQuery** 和 **\* BidiResponse** 元素 / **\*** ，如 PPD 文件中所指定。 请注意，必须仅为需要双向信息的功能添加这些元素。

2.  将 GDL 文件包含在与驱动程序相关的文件列表中。

本节包括：

[GPD 架构的新关键字](new-keyword-for-gpd-schema.md)

[Windows Vista 中 GPD 的自动配置流](autoconfiguration-flow-for-gpd-in-windows-vista.md)

[将构造添加到 GPD 的 GDL 文件](adding-constructs-to-your-gdl-file-for-gpd.md)

 

 




