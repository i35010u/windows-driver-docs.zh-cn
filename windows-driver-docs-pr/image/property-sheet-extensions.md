---
title: 属性表扩展
description: 属性表扩展
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1413fe8b02adbafe74dde9ae4a47b458e089c910
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96829630"
---
# <a name="property-sheet-extensions"></a>属性表扩展





"属性" 上下文菜单项可用于访问 "扫描仪" 和 "照相机" 控制面板文件夹中 (根项) 或我的电脑文件夹的设备。

照相机和扫描仪的属性表扩展还可以为特定映像获取会话提供用户界面，即，非根 **IWiaItem** 对象 (查看 Microsoft Windows SDK 文档) ，在用户使用默认扫描对话框时处于活动状态。 可以通过 "图像获取" 对话框上的 "高级属性" 或 "高级设置" 链接访问这些扩展。 当从属性的上下文菜单中选择某一操作时，WIA 将使用供应商提供的 **IShellExtInit** 和 **IShellPropSheetExt** 接口实现构造属性表 (参阅 Windows SDK 文档) 。

对于属性表和上下文菜单 UI 扩展，Windows SDK 文档中所述的 **IDataObject** 接口 () 描述选定项的内容使用 WIAItemNames 格式或 WIAItemPointer 格式。 这些格式及其格式名称在 *wiadevd* 中定义。

WIAItemNames 格式（其格式名为 CFSTR \_ WIAItemNames）返回一个 HGLOBAL，该格式指向以 null 结尾的 **IWiaItem** 标识符列表。 每个标识符的格式为 " &lt; 设备 id &gt; ：： &lt; 完整路径名称" &gt; 。 对于根项，完整路径名称部分为空。

Microsoft Windows XP 和更高版本支持 WIAItemPointer 格式。 格式名称为 CFSTR \_ WIAITEMPTR。 WIAItemPointer 格式返回 STGMEDIUM 结构 (在) 其 **tymed** 成员设置为 tymed ISTREAM 的 Windows SDK 文档中声明 \_ 。 当用户仅选择一个项目时，可以使用此格式。 属性表或上下文扩展可以对存储在 STGMEDIUM 结构中的 **IStream** 对象调用 **CoUnmarshalInterface** ，以检索 **IWiaItem** 接口。  (，请参阅 Windows SDK 文档，以获取 **CoUnmarshalInterface** 函数以及 **IStream** 和 **IWiaItem** 接口的说明。 ) 使用此格式时，属性表中的每一页都可以共享正确封送的 **IWiaItem** 接口，这在扫描过程中十分重要。

 

 




