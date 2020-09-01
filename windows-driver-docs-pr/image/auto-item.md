---
title: 自动项
description: 自动项
ms.assetid: 59f9b71b-e4bd-44a3-a4f2-dfea9f1045e2
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4d60a610973b3d26188450284ee50d6b2102797c
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189885"
---
# <a name="auto-item"></a>自动项


若要在 Windows 7 和更高版本中实现[自动配置的扫描](auto-configured-scanning.md)，wia 微型驱动程序必须在扫描仪设备的[WIA 项树](wia-item-trees.md)中包含一个*自动项*。 自动项属于 WIA \_ 类别 \_ 自动分类。 有关此类别的详细信息，请参阅 [WIA 项类别](wia-item-categories.md)。

下图显示了一个包含自动项的 WIA 项的示例。 自动项是树中根项的子项。

![说明包含自动项的项树的关系图](images/wia-feeder-tree5.png)

除了自动项外，上图中的 WIA 树还包括一个平台项和一个馈送器项，两者都是根项的子项。 WIA 体系结构要求自动项不是根项的唯一子级-自动项始终具有一个或多个同级。 其中至少一个同级必须是平板项目、送纸器项或胶卷项。 有关这些项的详细信息，请参阅 [WIA 项类别](wia-item-categories.md)。

如果 WIA 扫描器设备支持自动配置的扫描，则 WIA 应用程序可以通过从自动项请求数据传输从设备上当前选定的输入源中获取映像。 为响应此请求，设备可以在获取映像之前自动配置其大部分扫描设置。 应用程序只负责确定用于传输的文件格式。 出于此原因，自动项实现了一个相对较小的 WIA 属性子集，这些属性由完全可编程输入源的 WIA 项实现 (即，平板项、进纸器项或胶卷项) 。 有关详细信息，请参阅 [自动项支持的 WIA 属性](wia-properties-supported-by-an-auto-item.md)。

WIA 体系结构不允许处于自动配置的扫描模式下运行的扫描程序设备自动选择用于传输从输入源获取的图像数据的文件格式。 相反，应用程序将通过显式选择格式或只接受默认格式来确定文件格式。 此限制可防止设备以应用程序无法使用的格式传输扫描的图像数据。

支持自动配置扫描的扫描仪设备的 WIA 微型驱动程序应在 \_ wia 树中的根项实现的 [**wia \_ DPS \_ 文档 \_ 处理 \_ 功能**](./wia-dps-document-handling-capabilities.md) 属性值中设置自动源标志位。 WIA 应用程序可以查询此属性，以确定设备的 WIA 项树是否包含自动项。

 

