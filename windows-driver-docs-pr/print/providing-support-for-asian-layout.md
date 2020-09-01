---
title: 提供亚洲语言布局支持
description: 提供亚洲语言布局支持
ms.assetid: 38c7dfca-ce30-4967-84a4-e2f40bba8c57
keywords:
- 打印处理器 WDK，亚洲语言
- 亚洲语言 WDK 打印
- 手册 WDK 打印
- N 个打印 WDK
- 反向转换 WDK 打印
- 阿拉伯打印支持 WDK
- 日语打印支持 WDK
- 乌尔都语打印支持 WDK
- 国际化注意事项 WDK
- 打印亚洲语言 WDK
- 语言 WDK 打印
- 从右到左阅读语言 WDk 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9b50b7e3e39ed4fc037d57ac886a99feb07602d0
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89209489"
---
# <a name="providing-support-for-asian-layout"></a>提供亚洲语言布局支持


Microsoft Windows 打印处理器支持从右到左阅读的亚洲语言，如阿拉伯语、日语和乌尔都语，具有以下功能：

-   **N 向上方向**：在单张纸上打印多页时，用户可以按从右到左的顺序在工作表上打印页面。

-   **手册边缘**：打印小册子，其中折叠了页面并并排布局页面，用户可以从右到左排列页面。 下图显示了使用手册 \_ 边缘 \_ 右侧标志的手册页面布局。 ![使用手册 \- 边缘右侧标志说明手册页布局的关系图 \-](images/asian-booklet.png)

在 Windows Vista 中，可以使用标志更改驱动程序中的 N 向上方向和手册边缘以支持亚洲布局。 有关如何设置这些值的详细信息，请参阅 [**DrvQueryJobAttributes**](/windows-hardware/drivers/ddi/winddiui/nf-winddiui-drvqueryjobattributes) 和 [**属性 \_ 信息 \_ 4**](/windows-hardware/drivers/ddi/winddiui/ns-winddiui-_attribute_info_4)。

 

