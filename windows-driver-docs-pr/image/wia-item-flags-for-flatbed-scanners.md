---
title: 平板扫描仪的 WIA 项标志
description: 平板扫描仪的 WIA 项标志
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bccdecbca3642226f7fdb46dc5e36a6e8486787a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838263"
---
# <a name="wia-item-flags-for-flatbed-scanners"></a>平板扫描仪的 WIA 项标志





本主题列出了平台扫描器项树的根项和子项的必需和可选 WIA 项标志。 有关 WIA 项标志及其定义的完整列表，请参阅 [**wia \_ IPA \_ item \_ 标志**](./wia-ipa-item-flags.md)。

### <a name="required-wia-item-flags-for-flatbed-scanners"></a>平板扫描仪必需的 WIA 项标志

支持以下 WIA 项标志需要 WIA 平板扫描仪项：

<a href="" id="wiaitemtypeprogrammabledatasource"></a>**WiaItemTypeProgrammableDataSource**  
WIA 项是可配置的，并遵循一组基于 [**WIA \_ IPA \_ item \_ CATEGORY**](./wia-ipa-item-category.md) 属性的预定义配置规则。 此标志是必需的，因为扫描仪的平板部分是可编程的。

<a href="" id="wiaitemtypetransfer"></a>**WiaItemTypeTransfer**  
WIA 项可用于传输数据。 此标志是必需的，因为平板扫描仪项可用于传输数据。

<a href="" id="wiaitemtypefile"></a>**WiaItemTypeFile**  
该项是一个文件。 **WiaItemTypeImage** 标志需要此标志。

<a href="" id="wiaitemtypeimage"></a>**WiaItemTypeImage**  
该项是一个图像。 此标志仅对还设置了 **WiaItemTypeFile** 标志的项有效。 此标志是必需的，因为平板扫描仪会报告 [**WIA \_ IPA \_ 格式**](./wia-ipa-format.md) 属性值的图像格式。 所有 WIA 平板扫描仪项都需要至少支持一种图像格式。 WIA 当前需要 WiaImgFmt \_ BMP 和 WiaImgFmt \_ MEMORYBMP 作为支持的图像格式。

### <a name="optional-wia-item-flags-for-flatbed-scanners"></a>平板扫描仪的可选 WIA 项标志

WIA 平板扫描仪项可以选择支持以下 WIA 项标志：

<a href="" id="wiaitemtypefolder"></a>**WiaItemTypeFolder**  
该项是一个文件夹。 如果平板扫描仪项包含子项，请添加此标志。  (这些项可能会在单个平板影印上包含多个选定区域。 ) 只应在基础项上使用此标志。 子项目 *不能* 具有此标志。

 

