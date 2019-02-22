---
title: 属性表扩展插件
description: 属性表扩展插件
ms.assetid: 36254759-882c-45af-92df-e0769b65ec55
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 63e01c1fdbfacf01b6a39036b6131655f71e910e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56546809"
---
# <a name="property-sheet-extensions"></a>属性表扩展插件





属性上下文菜单项可以访问扫描仪或照相机属性表中任意一种扫描仪和照相机控件面板的设备 （根项） 的文件夹或我的电脑文件夹。

照相机和扫描仪的属性表扩展插件还可以提供用户界面针对特定的映像要掌握的会话，即，非根**IWiaItem**对象 （请参阅 Microsoft Windows SDK 文档），处于活动状态用户正在使用默认的扫描对话框。 这些扩展的访问通过高级属性或链接图像采集对话框上的高级的设置。 当从一个属性的上下文菜单中选择某项操作时，WIA 构造使用的供应商提供实现的属性表**IShellExtInit**并**IShellPropSheetExt**接口 （请参阅 Windows SDK 文档）。

对于这两个属性表和上下文菜单 UI 扩展， **IDataObject** （Windows SDK 文档中所述） 的接口描述所选的项使用 WIAItemNames 格式或 WIAItemPointer 格式。 中定义这些格式和其格式的名称*wiadevd.h*。

WIAItemNames 格式，其格式名称为 CFSTR\_WIAITEMNAMES，返回指向双 null 结尾的列表 HGLOBAL **IWiaItem**标识符。 每个标识符的形式&lt;设备 id&gt;::&lt;完整路径名称&gt;。 对于根项的完整路径名称部分为空。

版本的 Microsoft Windows XP 及更高版本中支持 WIAItemPointer 格式。 格式名称是 CFSTR\_WIAITEMPTR。 WIAItemPointer 格式返回 （在 Windows SDK 文档中声明） 的 STGMEDIUM 结构的**tymed**成员设置为 TYMED\_ISTREAM。 当用户选择单个项时，可以使用此格式。 属性表或上下文扩展可以调用**CoUnmarshalInterface**上**IStream**对象存储在 STGMEDIUM 结构检索**IWiaItem**接口。 (请参阅 Windows SDK 文档有关的说明**CoUnmarshalInterface**函数，并**IStream**并**IWiaItem**接口。)使用此格式，每一页上的属性表可以共享正确封送**IWiaItem**接口，在扫描期间很重要。

 

 




