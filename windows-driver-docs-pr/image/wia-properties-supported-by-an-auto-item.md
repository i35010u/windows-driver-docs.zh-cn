---
title: 自动项支持的 WIA 属性
description: 自动项支持的 WIA 属性
ms.assetid: 71b3a9ea-e402-4be8-9c62-9463e2a10f27
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a2d45a16ba6038bd941c7070c867782b11eca6e2
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67355171"
---
# <a name="wia-properties-supported-by-an-auto-item"></a>自动项支持的 WIA 属性


[自动项](auto-item.md)表示[自动配置扫描](auto-configured-scanning.md)WIA 设备的自动配置 WIA 应用程序的大部分而无需干预的扫描作业及其设置的函数。 有关自动项目的详细信息，请参阅 WIA 的讨论\_类别\_中的自动类别[WIA 项类别](wia-item-categories.md)。

WIA 服务管理自动项上的以下 WIA 属性：

[**WIA\_IPA\_ITEM\_NAME**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-name)

[**WIA\_IPA\_FULL\_ITEM\_NAME**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-full-item-name)

[**WIA\_IPA\_ITEM\_FLAGS**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-flags)

[**WIA\_IPA\_访问\_权限**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-access-rights)

[**WIA\_IPA\_颜色\_配置文件**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-color-profile)

WIA 服务初始化 WIA\_IPA\_项\_代表属性值设置为提交的微型驱动程序的项目名称微型驱动程序名称属性。 同样，WIA 服务初始化 WIA\_IPA\_项\_标志属性代表微型驱动程序通过将属性设置为提交的微型驱动程序的标志值。

WIA 微型驱动程序可以实现自动项上的以下属性：

[**WIA\_IPA\_项\_类别**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-category)

[**WIA\_IPA\_压缩**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-compression)

[**WIA\_IPA\_FILENAME\_EXTENSION**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-filename-extension)

[**WIA\_IPA\_格式**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-format)

[**WIA\_IPA\_PREFERRED\_FORMAT**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-preferred-format)

[**WIA\_IPA\_TYMED**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-tymed)

对于自动项，WIA 体系结构需要微型驱动程序支持的所有属性在上述列表中，除 WIA\_IPA\_文件名\_扩展。 支持 WIA\_IPA\_文件名\_扩展属性是可选的但建议执行。

微型驱动程序必须设置 WIA\_IPA\_项\_WIA 的值自动项类别属性\_类别\_自动。 在上述列表中的最后五个属性使 WIA 应用程序来协商用于将设备自动配置扫描期间获取的图像数据传输的文件格式。 应用程序应选择基于其内部的要求的文件格式。 某些应用程序可能会使用户能够从支持的应用程序和驱动程序的格式的列表中选择一种文件格式。

 

 




