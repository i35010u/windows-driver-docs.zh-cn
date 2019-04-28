---
title: 修改驱动程序提供的属性表页
description: 修改驱动程序提供的属性表页
ms.assetid: 98338017-96a0-414c-9b80-bcb98eff61e5
keywords:
- 用户界面插件 WDK 打印，属性表页
- UI 插件 WDK 打印，属性表页
- 属性表页 WDK 打印
- 选项项 WDK UI 插件
- 自定义的选项项 WDK UI 插件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1e9199b9e3eac555eab8be8ac9e11dfc463cc9c1
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63338316"
---
# <a name="modifying-a-driver-supplied-property-sheet-page"></a>修改驱动程序提供的属性表页





UI 插件可以通过实现来修改 Unidrv 提供或者 Pscript5 提供属性表页[ **IPrintOemUI::CommonUIProp** ](https://msdn.microsoft.com/library/windows/hardware/ff554159)方法和一个回调函数。

UI 插件用**IPrintOemUI::CommonUIProp**方法，以指定选项的一组项[CPSUI](common-property-sheet-user-interface.md)可以添加、 移除或替换中的打印机属性表**设备设置**页或文档属性表**布局**，**纸张/质量**，并且**高级**页。

类型的回调函数， [ **OEMCUIPCALLBACK**](https://msdn.microsoft.com/library/windows/hardware/ff557650)，用于处理的自定义的选项项目的用户修改。

### <a href="" id="ddk-adding-option-items-gg"></a>添加选项项

你的 UI 插件必须描述通过将它们放在一个数组中的新选项项[ **OPTITEM** ](https://msdn.microsoft.com/library/windows/hardware/ff559656)结构提供的驱动程序。 驱动程序的打印机接口 DLL 调用 UI 插件的[ **IPrintOemUI::CommonUIProp** ](https://msdn.microsoft.com/library/windows/hardware/ff554159)方法两次。 第一次调用方法时，它应返回所需的 OPTITEM 结构数。 驱动程序 OPTITEM 数组分配空间，并介绍了中的数组[ **OEMCUIPPARAM** ](https://msdn.microsoft.com/library/windows/hardware/ff557653)结构。 驱动程序调用**IPrintOemUI::CommonUIProp**同样，提供 OEMCUIPPARAM 结构的地址，因此该方法可以加载 OPTITEM 结构的选项说明。

### <a href="" id="ddk-removing-option-items-gg"></a>删除选项项

若要从由 Unidrv 或 Pscript5，在 UI 即插即用中的提供的属性表页中删除某个选项[ **IPrintOemUI::CommonUIProp** ](https://msdn.microsoft.com/library/windows/hardware/ff554159)方法可以遍历的数组[ **OPTITEM** ](https://msdn.microsoft.com/library/windows/hardware/ff559656)指向结构[ **OEMCUIPPARAM** ](https://msdn.microsoft.com/library/windows/hardware/ff557653)结构。 对于你想要从属性表中删除每个选项，可以设置 OPTITEM 结构 OPTIF\_隐藏标志。 (请注意，这不会实际删除选项; 它会隐藏从用户的选项，以便用户不能更改其默认值。)

### <a href="" id="ddk-replacing-option-items-gg"></a>选项的项目替换为

若要替换由 Unidrv 或 Pscript 提供的属性表页中的一个选项，应遵循下前面所示的说明**删除选项项**部分删除现有的选项项目，然后按照在前面的说明**添加选项项**部分，以创建新的选项选项用于替换旧。

### <a href="" id="ddk-handling-modifications-to-customized-option-values-gg"></a>处理对自定义的选项值的修改

要处理的自定义的选项项目的用户修改，必须提供至少一个回调函数。 您可以指定用于处理文档属性表和打印机属性页中，选项的单个回调函数，也可以为每个指定单独的函数。 这些回调属于类型[ **OEMCUIPCALLBACK**](https://msdn.microsoft.com/library/windows/hardware/ff557650)。

通过将放置在其地址指定一个回调函数[ **OEMCUIPPARAM** ](https://msdn.microsoft.com/library/windows/hardware/ff557653)结构。 UI 插件作为输入接收此结构的地址及其[ **IPrintOemUI::CommonUIProp** ](https://msdn.microsoft.com/library/windows/hardware/ff554159)方法。

当用户打开打印机属性表或文档属性表，并修改选项， [CPSUI](common-property-sheet-user-interface.md)调用打印机驱动程序的打印机接口 DLL。 此 DLL 处理包含在其自己的选项值[ **OPTITEM** ](https://msdn.microsoft.com/library/windows/hardware/ff559656)结构。 然后，每个插件的 UI，打印机接口 DLL 调用以前指定的类型 OEMCUIPCALLBACK 化回调函数**IPrintOemUI::CommonUIProp**。

 

 




