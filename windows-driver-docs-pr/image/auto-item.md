---
title: 自动项
description: 自动项
ms.assetid: 59f9b71b-e4bd-44a3-a4f2-dfea9f1045e2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 427d3a97509dcfe0f33eab186d234c32bf5c076a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366755"
---
# <a name="auto-item"></a>自动项


若要实现[自动配置扫描](auto-configured-scanning.md)WIA 微型驱动程序在 Windows 7 和更高版本，必须包括*自动项*中[WIA 项树](wia-item-trees.md)扫描程序设备。 自动项所属 WIA\_类别\_自动类别。 有关此类别的详细信息，请参阅[WIA 项类别](wia-item-categories.md)。

下图显示了包括自动项示例 WIA 项树。 自动项是在树中根项的子级。

![说明包括自动项的项树的关系图](images/wia-feeder-tree5.png)

除了自动项，在上图中的 WIA 树还包括平板项和送纸器项，这两个根项的子级。 WIA 体系结构需要自动项永远不会是唯一的子根项-的自动项始终有一个或多个同级。 这些同级至少必须是平板项、 送纸器项或电影项。 有关这些项目的详细信息，请参阅[WIA 项类别](wia-item-categories.md)。

如果 WIA 扫描程序设备支持自动配置扫描，WIA 应用程序可以获取在设备上当前所选的输入源中的映像，请求自动项数据传输。 对此请求的响应，设备才会获取该映像会自动可配置大多数其扫描设置。 应用程序负责只可用于确定要用于传输的文件格式。 出于此原因，自动项实现的 WIA 属性的完全可编程的输入源 （即，平板项、 送纸器项或电影项） 的 WIA 项由实现了相对较小部分。 有关详细信息，请参阅[WIA 属性支持的自动项](wia-properties-supported-by-an-auto-item.md)。

WIA 体系结构不允许在自动配置扫描模式下运行来自动选择它使用传输图像数据从输入源获取的文件格式的扫描程序设备。 相反，应用程序确定文件格式，那么，通过显式选择一种格式或只需接受默认格式。 此限制将阻止设备将传输扫描的图像格式的数据的应用程序不能使用。

WIA 微型驱动程序支持自动配置扫描的扫描程序设备应设置自动\_源标志位[ **WIA\_DPS\_文档\_处理\_功能**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-capabilities)由 WIA 树中的根项目实现的属性值。 WIA 应用程序可以查询此属性以确定是否在设备的 WIA 项树包含自动项。

 

 




