---
title: 特定于 PPD 的接口
description: 特定于 PPD 的接口
ms.assetid: 12d5baa2-4fd4-4eca-84c7-1ee168ee8259
keywords:
- 打印的 postScript 打印机驱动程序 WDK PPD 特定于接口
- Pscript WDK 打印、 特定于 PPD 的接口
- IPrintCoreUI2
- PPD 文件 WDK Pscript
- 特定于 PPD 的接口 WDK Pscript
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4f7debc40ac377db31bcd9b5a328b4237cbe0248
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67373803"
---
# <a name="ppd-specific-interface"></a>特定于 PPD 的接口





IPrintCoreUI2 COM 接口文件中。 六个这些方法中支持[IPrintCorePS2 COM 接口](iprintcoreps2-com-interface.md)。 本部分介绍这些方法的特定于 PPD 的行为。

### <a name="iprintcoreui2-interface-ppd-methods"></a>IPrintCoreUI2 接口 PPD 方法

[**IPrintCoreUI2::EnumConstrainedOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-enumconstrainedoptions)

[**IPrintCoreUI2::EnumFeatures**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-enumfeatures)

[**IPrintCoreUI2::EnumOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-enumoptions)

[**IPrintCoreUI2::GetOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-getoptions)

[**IPrintCoreUI2::GetFeatureAttribute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-getfeatureattribute)

[**IPrintCoreUI2::GetGlobalAttribute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-getglobalattribute)

[**IPrintCoreUI2::GetOptionAttribute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-getoptionattribute)

[**IPrintCoreUI2::SetOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-setoptions)

[**IPrintCoreUI2::WhyConstrained**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreui2-whyconstrained)

### <a name="iprintcoreps2-interface-ppd-methods"></a>IPrintCorePS2 接口 PPD 方法

[**IPrintCorePS2::EnumFeatures**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreps2-enumfeatures)

[**IPrintCorePS2::EnumOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreps2-enumoptions)

[**IPrintCorePS2::GetOptions**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreps2-getoptions)

[**IPrintCorePS2::GetFeatureAttribute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreps2-getfeatureattribute)

[**IPrintCorePS2::GetGlobalAttribute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreps2-getglobalattribute)

[**IPrintCorePS2::GetOptionAttribute**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/prcomoem/nf-prcomoem-iprintcoreps2-getoptionattribute)

在本部分中，对这两个接口成员的任何方法的引用适用于这两种方法。 例如，引用**GetOptions**适用于**IPrintCoreUI2::GetOptions** ，以及为**IPrintCorePS2::GetOptions**。

### <a name="ppd-feature-availability"></a>PPD 功能可用性

请注意，在此部分中，短语"PPD 功能不是当前可用的"意味着的打印机不支持该功能或功能的非-无/False 选项约束的可安装选项的当前设置。

例如，"双工功能当前不可"意味着未指定任一 PPD \***双工**功能关键字，则\***双工**关键字的功能非-None 选项当前受双面打印单元未安装的事实。

 

 




