---
title: 自动项支持的 WIA 属性
description: 自动项支持的 WIA 属性
ms.assetid: 71b3a9ea-e402-4be8-9c62-9463e2a10f27
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 995920193026fc1f5702cb4fe42ba27da6c2697b
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63352681"
---
# <a name="wia-properties-supported-by-an-auto-item"></a>自动项支持的 WIA 属性


[自动项](auto-item.md)表示[自动配置扫描](auto-configured-scanning.md)WIA 设备的自动配置 WIA 应用程序的大部分而无需干预的扫描作业及其设置的函数。 有关自动项目的详细信息，请参阅 WIA 的讨论\_类别\_中的自动类别[WIA 项类别](wia-item-categories.md)。

WIA 服务管理自动项上的以下 WIA 属性：

[**WIA\_IPA\_ITEM\_NAME**](https://msdn.microsoft.com/library/windows/hardware/ff551590)

[**WIA\_IPA\_FULL\_ITEM\_NAME**](https://msdn.microsoft.com/library/windows/hardware/ff551561)

[**WIA\_IPA\_ITEM\_FLAGS**](https://msdn.microsoft.com/library/windows/hardware/ff551585)

[**WIA\_IPA\_访问\_权限**](https://msdn.microsoft.com/library/windows/hardware/ff551518)

[**WIA\_IPA\_颜色\_配置文件**](https://msdn.microsoft.com/library/windows/hardware/ff551536)

WIA 服务初始化 WIA\_IPA\_项\_代表属性值设置为提交的微型驱动程序的项目名称微型驱动程序名称属性。 同样，WIA 服务初始化 WIA\_IPA\_项\_标志属性代表微型驱动程序通过将属性设置为提交的微型驱动程序的标志值。

WIA 微型驱动程序可以实现自动项上的以下属性：

[**WIA\_IPA\_项\_类别**](https://msdn.microsoft.com/library/windows/hardware/ff551581)

[**WIA\_IPA\_压缩**](https://msdn.microsoft.com/library/windows/hardware/ff551540)

[**WIA\_IPA\_FILENAME\_EXTENSION**](https://msdn.microsoft.com/library/windows/hardware/ff551549)

[**WIA\_IPA\_格式**](https://msdn.microsoft.com/library/windows/hardware/ff551553)

[**WIA\_IPA\_PREFERRED\_FORMAT**](https://msdn.microsoft.com/library/windows/hardware/ff551623)

[**WIA\_IPA\_TYMED**](https://msdn.microsoft.com/library/windows/hardware/ff551656)

对于自动项，WIA 体系结构需要微型驱动程序支持的所有属性在上述列表中，除 WIA\_IPA\_文件名\_扩展。 支持 WIA\_IPA\_文件名\_扩展属性是可选的但建议执行。

微型驱动程序必须设置 WIA\_IPA\_项\_WIA 的值自动项类别属性\_类别\_自动。 在上述列表中的最后五个属性使 WIA 应用程序来协商用于将设备自动配置扫描期间获取的图像数据传输的文件格式。 应用程序应选择基于其内部的要求的文件格式。 某些应用程序可能会使用户能够从支持的应用程序和驱动程序的格式的列表中选择一种文件格式。

 

 




