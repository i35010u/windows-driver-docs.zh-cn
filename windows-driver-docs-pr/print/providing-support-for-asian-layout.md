---
title: 提供亚洲语言布局支持
description: 提供亚洲语言布局支持
ms.assetid: 38c7dfca-ce30-4967-84a4-e2f40bba8c57
keywords:
- 打印处理器 WDK，亚洲语言
- 亚洲语言 WDK 打印
- 打印手册 WDK 的步骤
- 每张多打印 WDK
- 反转方向打印的 WDK
- 阿拉伯语打印支持 WDK
- 日语打印支持 WDK
- 乌尔都语打印支持 WDK
- WDK 的国际注意事项
- 打印亚洲语言 WDK
- 语言 WDK 打印
- 从右到左的读取语言 WDk 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d8aa3bddaa2035af7e152e6269fd8e9e687d95c4
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67356008"
---
# <a name="providing-support-for-asian-layout"></a>提供亚洲语言布局支持


Microsoft Windows 打印处理器支持亚洲语言读取从右到左，如阿拉伯语、 日语和乌尔都语，具有以下功能：

-   **每张多方向**:在单张纸上打印多页，用户可以打印工作表上从右到左的顺序的页。

-   **手册边缘**:当打印的手册，在其中折叠表和页布局的并排方案，用户可以订购从右到左的手册页。 下图显示使用手册手册的页面布局\_EDGE\_右标志。![使用手册说明手册的页面布局的关系图\-边缘\-右键标志](images/asian-booklet.png)

Windows Vista 中提供了使您能够更改驱动程序以支持中文版式中的每张多方向和手册边缘的标志。 有关如何设置这些值的详细信息，请参阅[ **DrvQueryJobAttributes** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/nf-winddiui-drvqueryjobattributes)并[**属性\_信息\_4** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/winddiui/ns-winddiui-_attribute_info_4).

 

 




