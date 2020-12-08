---
title: WIA 项标志
description: WIA 项标志
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cdfe421127dc6bf0ff60274d355c22ed11f2ef0b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96824091"
---
# <a name="wia-item-flags"></a>WIA 项标志





本主题适用于 Windows Vista 和更高版本。

WIA 项标志用于帮助对特定 WIA 项的内容或支持的行为进行分类。 WIA 项目标志分为两个基本组：

<a href="" id="item-status-flags"></a>项状态标志  
报告 WIA 项的当前状态的标志。

例如： **WiaItemTypeDisconnected**、 **WiaItemTypeDeleted** 等。

<a href="" id="item-data-representation-usage-flags"></a>项数据表示/用法标志  
报告 WIA 项表示或可以在传输时生成的数据的标志。

例如： **WiaItemTypeImage** 是一个数据表示标志，该标志通知应用程序与当前 WIA 项关联的数据是图像数据，并且应具有图像数据属性。 **WiaItemTypeProgrammableDataSource** 是一个项目使用标志，该标志告知应用程序 wia 项可配置，遵循 [**wia \_ IPA \_ 项 \_ 类别**](./wia-ipa-item-category.md)上一组预定义的配置规则，并且该配置可能会更改每个数据传输的结果。 有关类别定义的详细信息，请参阅 [WIA 项类别](wia-item-categories.md) 。

有关 WIA 项标志及其定义的完整列表，请参阅 [**wia \_ IPA \_ item \_ 标志**](./wia-ipa-item-flags.md)。

 

