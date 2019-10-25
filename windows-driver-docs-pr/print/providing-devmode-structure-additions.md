---
title: 提供 DEVMODE 结构补充
description: 提供 DEVMODE 结构补充
ms.assetid: 7ce698f5-14c7-484d-be3d-b41c690b9576
keywords:
- 用户界面插件 WDK 打印，DEVMODEW 结构添加
- UI 插件 WDK 打印，DEVMODEW 结构添加件
- DEVMODEW
- 私有 DEVMODE WDK 打印
- 公共 DEVMODE WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c672b63dc5a671c32724b2abd4b269389addca2e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840421"
---
# <a name="providing-devmode-structure-additions"></a>提供 DEVMODE 结构补充





UI 插件可以将其自己的私有成员添加到[**DEVMODEW**](https://docs.microsoft.com/windows/desktop/api/wingdi/ns-wingdi-_devicemodew)结构中，如下图所示。

![阐释公有和私有 devmode 部分的示意图](images/dvmdstru.png)

UI 插件可以使用这些专用 DEVMODE 成员来存储与自定义打印机选项关联的值。 此插件通过[修改驱动程序提供的属性表页](modifying-a-driver-supplied-property-sheet-page.md)或通过[添加新的属性表页](adding-new-property-sheet-pages.md)，使用户可以使用这些选项。

如果 UI 插件添加了私有 DEVMODE 成员，则[**OEM\_DMEXTRAHEADER**](https://docs.microsoft.com/windows-hardware/drivers/ddi/printoem/ns-printoem-_oem_dmextraheader)结构必须为添加的成员添加前缀。

不需要将成员添加到 DEVMODE 结构，但如果这样做，UI 插件必须实现[**IPrintOemUI：:D evmode**](https://docs.microsoft.com/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-devmode)方法。 此方法的目的是返回、初始化、转换或验证附加的 DEVMODE 成员，具体取决于输入参数。

 

 




