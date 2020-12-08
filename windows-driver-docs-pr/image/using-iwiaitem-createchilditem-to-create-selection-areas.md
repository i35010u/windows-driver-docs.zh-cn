---
title: 使用 IWiaItem CreateChildItem 创建选择区域
description: 使用 IWiaItem CreateChildItem 创建选择区域
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dde647bbb11265426553bcd059d96322512718d9
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827081"
---
# <a name="using-iwiaitemcreatechilditem-to-create-selection-areas"></a>使用 IWiaItem::CreateChildItem 创建选择区域





WIA 应用程序应阅读 " [**wia \_ IPS \_ 支持 \_ 子 \_ 项目 \_ 创建**](./wia-ips-supports-child-item-creation.md) " 属性，以确定胶卷扫描项是否支持创建子项。 胶片扫描器项可以包含子项 (也就是说，项树中 *无法* 删除的帧) 。 应用程序可以删除标记为 (WIA 内容读取的 [**wia \_ IPA \_ 访问 \_ 权限**](./wia-ipa-access-rights.md) 设置的 wia 项 \_ \_ |WIA \_ 项 \_ 写入 |\_ \_ 可以 \_ \_) 删除 WIA 项。

### <a name="creating-dynamic-film-items"></a>创建动态胶片项

WIA 应用程序会调用 Microsoft Windows SDK 文档) 中所述的 **IWiaItem：： CreateChildItem** (来创建位于 "胶片扫描器" 项下的新 WIA 应用程序项 (或帧) 。 WIA 驱动程序应初始化必需的 WIA 属性，WIA 应用程序应设置范围设置和任何其他属性来配置新帧。 有关所需的 WIA 属性的详细信息，请参阅 [胶卷扫描器的必需 Wia 项目属性](required-wia-item-properties-for-film-scanners.md)。

**注意**   WIA 胶卷项必须只有一级子项目。 胶片项可以设置为文件夹，但 *不能* 在 "胶片扫描器" 项下创建文件夹项。

 

 

