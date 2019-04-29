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
ms.openlocfilehash: 99db8f3645f569daff11cbc767fdd81a0585841a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63389546"
---
# <a name="ppd-specific-interface"></a>特定于 PPD 的接口





IPrintCoreUI2 COM 接口文件中。 六个这些方法中支持[IPrintCorePS2 COM 接口](iprintcoreps2-com-interface.md)。 本部分介绍这些方法的特定于 PPD 的行为。

### <a name="iprintcoreui2-interface-ppd-methods"></a>IPrintCoreUI2 接口 PPD 方法

[**IPrintCoreUI2::EnumConstrainedOptions**](https://msdn.microsoft.com/library/windows/hardware/ff553045)

[**IPrintCoreUI2::EnumFeatures**](https://msdn.microsoft.com/library/windows/hardware/ff553050)

[**IPrintCoreUI2::EnumOptions**](https://msdn.microsoft.com/library/windows/hardware/ff553052)

[**IPrintCoreUI2::GetOptions**](https://msdn.microsoft.com/library/windows/hardware/ff553069)

[**IPrintCoreUI2::GetFeatureAttribute**](https://msdn.microsoft.com/library/windows/hardware/ff553056)

[**IPrintCoreUI2::GetGlobalAttribute**](https://msdn.microsoft.com/library/windows/hardware/ff553059)

[**IPrintCoreUI2::GetOptionAttribute**](https://msdn.microsoft.com/library/windows/hardware/ff553064)

[**IPrintCoreUI2::SetOptions**](https://msdn.microsoft.com/library/windows/hardware/ff553081)

[**IPrintCoreUI2::WhyConstrained**](https://msdn.microsoft.com/library/windows/hardware/ff553087)

### <a name="iprintcoreps2-interface-ppd-methods"></a>IPrintCorePS2 接口 PPD 方法

[**IPrintCorePS2::EnumFeatures**](https://msdn.microsoft.com/library/windows/hardware/ff552990)

[**IPrintCorePS2::EnumOptions**](https://msdn.microsoft.com/library/windows/hardware/ff552996)

[**IPrintCorePS2::GetOptions**](https://msdn.microsoft.com/library/windows/hardware/ff553019)

[**IPrintCorePS2::GetFeatureAttribute**](https://msdn.microsoft.com/library/windows/hardware/ff553006)

[**IPrintCorePS2::GetGlobalAttribute**](https://msdn.microsoft.com/library/windows/hardware/ff553009)

[**IPrintCorePS2::GetOptionAttribute**](https://msdn.microsoft.com/library/windows/hardware/ff553013)

在本部分中，对这两个接口成员的任何方法的引用适用于这两种方法。 例如，引用**GetOptions**适用于**IPrintCoreUI2::GetOptions** ，以及为**IPrintCorePS2::GetOptions**。

### <a name="ppd-feature-availability"></a>PPD 功能可用性

请注意，在此部分中，短语"PPD 功能不是当前可用的"意味着的打印机不支持该功能或功能的非-无/False 选项约束的可安装选项的当前设置。

例如，"双工功能当前不可"意味着未指定任一 PPD \***双工**功能关键字，则\***双工**关键字的功能非-None 选项当前受双面打印单元未安装的事实。

 

 




