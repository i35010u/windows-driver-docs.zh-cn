---
title: 使用 IWiaItem CreateChildItem 创建所选内容区域
description: 使用 IWiaItem CreateChildItem 创建所选内容区域
ms.assetid: c430d15b-51e9-4419-9cdb-904a0f5ef09b
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1abebae6edb22e25d618641d21735ef035ba8079
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56527174"
---
# <a name="using-iwiaitemcreatechilditem-to-create-selection-areas"></a>使用 IWiaItem::CreateChildItem 创建所选内容区域





WIA 应用程序应阅读[ **WIA\_IPS\_支持\_子\_项\_创建**](https://msdn.microsoft.com/library/windows/hardware/ff552653)属性来确定是否扫描项电影支持创建的子项目。 电影扫描程序项可以包含在该项目中的子项目 （即，帧） 树*不能*被删除。 应用程序可以删除与标记的 WIA 项[ **WIA\_IPA\_访问\_RIGHTS** ](https://msdn.microsoft.com/library/windows/hardware/ff551518)的设置 (WIA\_PROP\_读取 |WIA\_项\_编写 |WIA\_项\_可以\_BE\_已删除)。

### <a name="creating-dynamic-film-items"></a>创建动态电影项

WIA 应用程序调用**IWiaItem::CreateChildItem** （Microsoft Windows SDK 文档中所述） 来创建新的 WIA 应用程序项目 （或帧） 下的电影胶片扫描程序项。 WIA 驱动程序应初始化所需的 WIA 属性并 WIA 应用程序应设置的范围设置和任何其他属性来配置新帧。 有关所需的 WIA 属性的详细信息，请参阅[电影扫描程序所必需的 WIA 项属性](required-wia-item-properties-for-film-scanners.md)。

**请注意**   WIA 电影项必须只有一个级别的 WIA 子项目。 电影项可以被设置为一个文件夹中，但文件夹项*不能*电影扫描程序项下创建。

 

 

 




