---
title: 将 GDL 扩展添加到现有的 GPD 文件
description: 将 GDL 扩展添加到现有的 GPD 文件
ms.assetid: 5ba2a447-e133-47bb-aa1e-93abe75c6eef
keywords:
- 框中自动配置支持 WDK 打印机，GDL 扩展
- GDL 文件 WDK 打印机
- 扩展 WDK GDL 文件
- GPD 文件 WDK GDL 扩展
- GPD 文件 WDK GDL 扩展添加
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0203fdc2e83181272e8ebf43e658df2a224a43c2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63341331"
---
# <a name="adding-gdl-extensions-to-an-existing-gpd-file"></a>将 GDL 扩展添加到现有的 GPD 文件


如果你想要将自动配置的支持添加到现有现成 GPD 文件，您应该：

1.  创建 GDL 文件。 GDL 文件应具有 **\*BidiQuery**并 **\*BidiResponse**对应的元素 **\*功能**/ **\*选项**构造 PPD 文件中指定。 请注意，必须添加这些元素仅对需要 bidi 信息的功能。

2.  包括 GDL 文件依赖于驱动程序的文件列表的一部分。

本部分包括：

[新关键字 GPD 架构](new-keyword-for-gpd-schema.md)

[Windows Vista 中的 GPD 的自动配置流](autoconfiguration-flow-for-gpd-in-windows-vista.md)

[添加构造 GPD GDL 文件](adding-constructs-to-your-gdl-file-for-gpd.md)

 

 




