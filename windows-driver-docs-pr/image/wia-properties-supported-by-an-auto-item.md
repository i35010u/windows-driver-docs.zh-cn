---
title: 自动项支持的 WIA 属性
description: 自动项支持的 WIA 属性
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9805548f592c0d0733ca1c8779c8eb913f69ef82
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826475"
---
# <a name="wia-properties-supported-by-an-auto-item"></a>自动项支持的 WIA 属性


[自动项](auto-item.md)表示 wia 设备的[自动配置扫描](auto-configured-scanning.md)功能，该功能可以自动为扫描作业配置大部分设置，而无需 WIA 应用程序进行干预。 有关自动项的详细信息，请参阅 \_ \_ [wia 项类别](wia-item-categories.md)中的 wia 类别自动分类的讨论。

WIA 服务管理自动项的以下 WIA 属性：

[**WIA \_ IPA \_ 项 \_ 名称**](./wia-ipa-item-name.md)

[**WIA \_ IPA \_ 完整 \_ 项 \_ 名称**](./wia-ipa-full-item-name.md)

[**WIA \_ IPA \_ 项 \_ 标志**](./wia-ipa-item-flags.md)

[**WIA \_ IPA \_ 访问 \_ 权限**](./wia-ipa-access-rights.md)

[**WIA \_ IPA \_ 颜色 \_ 配置文件**](./wia-ipa-color-profile.md)

WIA 服务 \_ \_ \_ 通过将属性值设置为微型驱动程序提交的项名称来代表微型驱动程序初始化 wia IPA ITEM NAME 属性。 同样，WIA 服务 \_ \_ \_ 通过将属性设置为微型驱动程序提交的 FLAGS 值来代表微型驱动程序初始化 wia IPA ITEM FLAGS 属性。

WIA 微型驱动程序可以实现自动项的以下属性：

[**WIA \_ IPA \_ 项 \_ 类别**](./wia-ipa-item-category.md)

[**WIA \_ IPA \_ 压缩**](./wia-ipa-compression.md)

[**WIA \_ IPA \_ 文件 \_ 扩展名**](./wia-ipa-filename-extension.md)

[**WIA \_ IPA \_ 格式**](./wia-ipa-format.md)

[**WIA \_ IPA \_ 首选 \_ 格式**](./wia-ipa-preferred-format.md)

[**WIA \_ IPA \_ TYMED**](./wia-ipa-tymed.md)

对于自动项，WIA 体系结构要求微型驱动程序支持前面列表中的所有属性，WIA \_ IPA \_ 文件 \_ 扩展名除外。 支持 WIA \_ IPA \_ FILENAME \_ EXTENSION 属性，但建议使用它。

微型驱动程序必须将 \_ 自动项的 wia IPA \_ 项 \_ CATEGORY 属性设置为值 WIA \_ 类别 \_ auto。 前面的列表中的最后五个属性使 WIA 应用程序能够协商用于传输设备在自动配置的扫描过程中获取的图像数据的文件格式。 应用程序应根据其内部要求选择一种文件格式。 某些应用程序可能允许用户从应用程序和驱动程序支持的格式列表中选择一种文件格式。

 

