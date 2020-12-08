---
title: 将 GDL 扩展添加到现有的 PPD 文件
description: 将 GDL 扩展添加到现有的 PPD 文件
keywords:
- 内置自动配置支持 WDK 打印机，GDL 扩展
- GDL 文件 WDK 打印机
- 扩展 WDK GDL 文件
- PPD 文件 WDK 自动配置，GDL 扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9f4459a20510e56d72e89618a4b01956e272193c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96794219"
---
# <a name="adding-gdl-extensions-to-an-existing-ppd-file"></a>将 GDL 扩展添加到现有的 PPD 文件


如果要将自动配置的支持添加到现有的内置 PPD 文件中，请执行以下步骤：

1.  创建 GDL 文件。 GDL 文件应具有与 \* **BidiQuery** \* *_BidiResponse_* \* *_Feature_* / \* PPD 文件中指定的功能 *_选项_* 构造对应的 BidiQuery 和 BidiResponse 元素。 请注意，必须仅对需要双向信息的功能执行此操作。

2.  将 GDL 文件作为驱动程序依赖文件列表的一部分包含在内。

本节包括：

[PPD 架构的新关键字](new-keyword-for-ppd-schema.md)

[Windows Vista 中的 PPD 自动配置流](autoconfig-flow-in-windows-vista-for-ppd.md)

[将构造添加到 PPD 的 GDL 文件](adding-constructs-to-your-gdl-file-for-ppd.md)

 

 




