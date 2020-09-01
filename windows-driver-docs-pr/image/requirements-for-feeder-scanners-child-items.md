---
title: 送纸器扫描仪子项的要求
description: 送纸器扫描仪子项的要求
ms.assetid: 069ce228-ac73-42b5-9f1b-528ee6fe6a92
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab7d9dfd10be574bf8db47a3adbab38e1aec7b88
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188063"
---
# <a name="requirements-for-feeder-scanners-child-items"></a>送纸器扫描仪子项的要求


进纸器扫描器项树中的子项 (也就是支持 (的) 项属性和标记的顶层和背面项) ，后者是支持的前项和后项的父项。

### <a name="item-flags"></a>项标志

子项目必须支持父项支持的所有必需项标志（ **WiaItemTypeTransfer**除外）。 可以选择支持 **WiaItemTypeTransfer** 标志;但是，从自动文档送纸器传输的数据是从送纸器项而不是子项目中完成的。

### <a name="item-properties"></a>项属性

馈送器扫描器项树中的子项 (或前一项和后一项) 是支持父送纸器项支持的大多数项属性所必需的。 子项目必须支持 " [**wia \_ IPA \_ item" \_ 类别**](./wia-ipa-item-category.md)和 " \_ \_ 输送器" 项支持的所有 wia ip*Xxx*和 wia \_ IPA \_ *Xxx*属性，这与扫描当前文档端的配置参数相关。 这些属性同时包括送纸器项的必需属性和可选属性。 扫描仪执行高级双工扫描时，将会使用子项目上设置的 "图像质量设置" (或扫描配置参数) ，并忽略在 "送纸器" 项上设置的设置。

**注意**   子项目的属性项设置必须与父项属性的设置相匹配。 唯一的例外是子项的 [**wia \_ IPA \_ ITEM \_ CATEGORY**](./wia-ipa-item-category.md) 属性; 此属性必须设置为 wia 类别进纸器 \_ \_ \_ 前端或 wia 类别 \_ \_ \_ \_ \_ 送纸器，而不是 wia 类别送纸器。

 

 

