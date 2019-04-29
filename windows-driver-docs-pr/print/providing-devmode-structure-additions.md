---
title: 提供 DEVMODE 结构补充
description: 提供 DEVMODE 结构补充
ms.assetid: 7ce698f5-14c7-484d-be3d-b41c690b9576
keywords:
- 接口插件 WDK 打印，DEVMODEW 结构添加用户
- UI 插件 WDK 打印，DEVMODEW 结构新增功能
- DEVMODEW
- 专用 DEVMODE WDK 打印
- 公共 DEVMODE WDK 打印
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 21a89551be81348cf9bdd95529fc8b5ca02ca167
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63376573"
---
# <a name="providing-devmode-structure-additions"></a>提供 DEVMODE 结构补充





你的 UI 插件可以添加到它自己的私有成员[ **DEVMODEW** ](https://msdn.microsoft.com/library/windows/hardware/ff552837)结构，如下图中所示。

![说明公钥和私钥 devmode 部分的关系图](images/dvmdstru.png)

UI 插件可以使用这些专用的 DEVMODE 成员来存储与自定义的打印机选项相关联的值。 该插件使这些选项可供用户通过[修改驱动程序所提供的属性表页](modifying-a-driver-supplied-property-sheet-page.md)或通过[添加新属性表页](adding-new-property-sheet-pages.md)。

如果你的 UI 插件添加专用的 DEVMODE 成员[ **OEM\_DMEXTRAHEADER** ](https://msdn.microsoft.com/library/windows/hardware/ff559588)结构必须前缀所添加的成员。

您不必将成员添加到 DEVMODE 结构，但如果这样做，必须实现您的 UI 插件[ **IPrintOemUI::DevMode** ](https://msdn.microsoft.com/library/windows/hardware/ff554167)方法。 此方法的用途，具体取决于输入参数是返回的大小、 初始化、 转换，或验证其他的 DEVMODE 成员。

 

 




