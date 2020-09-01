---
title: 底片扫描仪的 WIA 项标志
description: 底片扫描仪的 WIA 项标志
ms.assetid: 50aad730-6897-488d-a9de-58ce24738c17
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f4ad85d720c4c847688b3923b6353399e6b3a5a7
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89184467"
---
# <a name="wia-item-flags-for-film-scanners"></a>底片扫描仪的 WIA 项标志





本主题列出了扫描仪胶卷项的必需 WIA 项标志，以及 (的帧) 的扫描仪胶卷子项。 有关 WIA 项标志及其定义的完整列表，请参阅 [**wia \_ IPA \_ item \_ 标志**](./wia-ipa-item-flags.md)。

### <a name="required-wia-item-flags-for-film-scanners"></a>用于胶片扫描器的必需 WIA 项标志

需要 WIA 胶片扫描器项来支持以下 WIA 项标志：

<a href="" id="wiaitemtypeprogrammabledatasource"></a>**WiaItemTypeProgrammableDataSource**  
WIA 项是可配置的，并遵循一组基于 [**WIA \_ IPA \_ item \_ CATEGORY**](./wia-ipa-item-category.md) 属性的预定义配置规则。 此标志是必需的，因为扫描程序的胶片扫描部分是可编程的。

<a href="" id="wiaitemtypetransfer"></a>**WiaItemTypeTransfer**  
WIA 项可用于传输数据。 此标志是必需的，因为扫描仪的胶卷项可用于传输数据。

<a href="" id="wiaitemtypefile"></a>**WiaItemTypeFile**  
该项是一个文件。 **WiaItemTypeImage**标志需要此标志。

<a href="" id="wiaitemtypeimage"></a>**WiaItemTypeImage**  
该项是一个图像。 需要此标志，因为胶片扫描器会报告 [**WIA \_ IPA \_ 格式**](./wia-ipa-format.md) 属性值的图像格式。  (WIA 要求所有胶片扫描器项至少支持一种图像格式。 ) WIA 当前要求 \_ 支持 WiaImgFmt BMP 和 WiaImgFmt \_ MEMORYBMP 图像格式。

<a href="" id="wiaitemtypefolder"></a>**WiaItemTypeFolder**  
该项是一个文件夹。 根胶卷项需要此标志，以允许枚举单个帧子项目。  (帧表示单个胶卷扫描图面上的多个选定区域。 ) 扫描器电影子项 (帧) *不能* 有此标志。

 

