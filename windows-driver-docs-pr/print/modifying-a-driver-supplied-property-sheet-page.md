---
title: 修改驱动程序提供的属性表页
description: 修改驱动程序提供的属性表页
ms.assetid: 98338017-96a0-414c-9b80-bcb98eff61e5
keywords:
- 用户界面插件 WDK 打印，属性表页面
- UI 插件 WDK 打印，属性表单页面
- 属性表页 WDK 打印
- 选项项 WDK UI 插件
- 自定义选项项 WDK UI 插件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 37bc52aec39324e4df4ca8a47b84d908875359b2
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89210001"
---
# <a name="modifying-a-driver-supplied-property-sheet-page"></a>修改驱动程序提供的属性表页





UI 插件可以通过实现 [**IPrintOemUI：： CommonUIProp**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-commonuiprop) 方法和回调函数来修改 Unidrv 提供的或 Pscript5 的属性表页。

UI 插件使用 **IPrintOemUI：： CommonUIProp** 方法来指定一组选项项， [CPSUI](common-property-sheet-user-interface.md) 可以在打印机属性表的 " **设备设置** " 页或 "文档" 属性表的 " **布局**"、" **纸张/质量**" 页和 " **高级** " 页中添加、移除或替换。

类型为 [**OEMCUIPCALLBACK**](/windows-hardware/drivers/ddi/printoem/nc-printoem-oemcuipcallback)的回调函数用于处理用户对自定义选项项的修改。

### <a name="adding-option-items"></a><a href="" id="ddk-adding-option-items-gg"></a>添加选项项

用户的 UI 插件必须通过将新的选项放入驱动程序提供的 [**OPTITEM**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_optitem) 结构数组中来描述新的选项项。 驱动程序的打印机接口 DLL 调用 UI 插件的 [**IPrintOemUI：： CommonUIProp**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-commonuiprop) 方法两次。 第一次调用方法时，它应返回所需的 OPTITEM 结构的数量。 驱动程序为 OPTITEM 数组分配空间，并描述 [**OEMCUIPPARAM**](/windows-hardware/drivers/ddi/printoem/ns-printoem-_oemcuipparam) 结构中的数组。 驱动程序再次调用 **IPrintOemUI：： CommonUIProp** ，同时提供 OEMCUIPPARAM 结构的地址，因此该方法可以加载包含选项说明的 OPTITEM 结构。

### <a name="removing-option-items"></a><a href="" id="ddk-removing-option-items-gg"></a>删除选项项

若要从 Unidrv 或 Pscript5 提供的属性表页中删除选项，UI 插件的[**IPrintOemUI：： CommonUIProp**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-commonuiprop)方法可以遍历[**OPTITEM**](/windows-hardware/drivers/ddi/printoem/ns-printoem-_oemcuipparam)结构指向的[**OEMCUIPPARAM**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_optitem)结构的数组。 对于想要从属性表中删除的每个选项，可以设置 OPTITEM 结构的 OPTIF \_ 隐藏标志。  (请注意，这实际上不会删除该选项;它将从用户中隐藏选项，使用户无法更改其默认值。 ) 

### <a name="replacing-option-items"></a><a href="" id="ddk-replacing-option-items-gg"></a>替换选项项

若要替换 Unidrv 或 Pscript 提供的属性表页中的选项，应按照前面的 " **删除选项项** " 部分中显示的说明删除现有选项项，然后按照前面的 " **添加选项项** " 部分中的说明创建新的选项项来替换旧的选项。

### <a name="handling-modifications-to-customized-option-values"></a><a href="" id="ddk-handling-modifications-to-customized-option-values-gg"></a>处理对自定义选项值的修改

为了处理用户对自定义选项项的修改，您必须至少提供一个回调函数。 您可以指定处理文档属性表和打印机属性表的选项的单个回调函数，也可以为每个函数指定单独的函数。 这些回调的类型为 [**OEMCUIPCALLBACK**](/windows-hardware/drivers/ddi/printoem/nc-printoem-oemcuipcallback)。

通过将回调函数的地址放置在 [**OEMCUIPPARAM**](/windows-hardware/drivers/ddi/printoem/ns-printoem-_oemcuipparam) 结构中来指定该函数。 UI 插件接收此结构的地址作为其 [**IPrintOemUI：： CommonUIProp**](/windows-hardware/drivers/ddi/prcomoem/nf-prcomoem-iprintoemui-commonuiprop) 方法的输入。

当用户打开打印机属性表或文档属性表并修改选项时， [CPSUI](common-property-sheet-user-interface.md) 将调用打印机驱动程序的打印机接口 DLL。 此 DLL 处理其自身 [**OPTITEM**](/windows-hardware/drivers/ddi/compstui/ns-compstui-_optitem) 结构中包含的选项值。 然后，对于每个 UI 插件，打印机接口 DLL 将调用先前由 **IPrintOemUI：： CommonUIProp**指定的 OEMCUIPCALLBACK 类型的回调函数。

 

