---
title: 平板扫描仪的基本扫描
description: 平板扫描仪的基本扫描
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b841e8faa5070b044cddd44a0cbba09428b25ff5
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818423"
---
# <a name="basic-scanning-for-flatbed-scanners"></a>平板扫描仪的基本扫描





WIA 应用程序枚举 "扫描程序" 项树中的根项和顶级子项，以确定扫描程序的支持功能。 然后，应用程序使用此子项作为扫描源。 例如，平板扫描仪项用于从平板扫描，而送纸器项用于从文档送纸器进行扫描等等。

Windows Vista 中的 "平板" 项的编程和扫描行为与 Windows XP 和 Windows Me 使用的重载系统相同。 此重载系统通过将所有 WIA 特性标记放在项树中来计划第一个子项。

当应用程序在计划扫描仪的平台时（但不一定按顺序），通常会执行以下操作：

-   枚举顶级 WIA 项，查找标记有 **WiaItemTypeProgrammableDataSource** item 标志并将 [**wia \_ IPA \_ ITEM \_ CATEGORY**](./wia-ipa-item-category.md) 属性设置为 wia 类别 "平台" 的项 \_ \_ 。

-   读取 [**wia \_ IPA \_ TYMED**](./wia-ipa-tymed.md) 和 [**wia \_ IPA \_ 格式**](./wia-ipa-format.md) 属性的有效值。

-   通过设置 WIA \_ IPA TYMED 属性，选择内存传输或文件传输类型 \_ 。 有关可用传输类型的详细信息，请参阅 [数据传输](data-transfers.md)。 对于基于 **IStream** 的传输， \_ 默认情况下，WIA IPA \_ TYMED 设置为 TYMED \_ 文件，不应更改。

-   通过设置 WIA \_ IPA format 属性来选择数据的最终格式 \_ 。

-   选择图像设置，如 [**wia \_ IPA \_ DEPTH**](./wia-ipa-depth.md) 和 [**wia \_ IPA \_ DATATYPE**](./wia-ipa-datatype.md)。

-   使用此 WIA 项传输数据。

当驱动程序使用扫描程序的平板扫描时，驱动程序通常会执行以下操作：

1.  调用 [**IWiaMiniDrv：:D rvvalidateitemproperties**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties) 和 [**IWiaMiniDrv：:d rvreaditemproperties**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvreaditemproperties)。 WIA 驱动程序应在应用程序的属性设置阶段验证所有属性设置。

2.  调用 [**IWiaMiniDrv：:D rvwriteitemproperties**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvwriteitemproperties)。 传入的 WIA 项上下文属于平板扫描仪项，因此该驱动程序知道该应用程序要使用扫描程序的平台扫描。

3.  调用 [**IWiaMiniDrv：:D rvacquireitemdata**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)。 传入的 WIA 项上下文属于平板扫描仪项，因此驱动程序可以轻松确定应用程序打算使用平板影印进行扫描。

4.  使用当前的平台项属性对设备进行编程，并使用当前平台进行扫描。 如果 WIA 驱动程序未处于平板扫描模式，则它应尝试切换到此模式以进行扫描。 对于应用程序，没有任何特殊的设置可切换为使用平台。 使用 "平板" 项进行扫描是指应用程序与驱动程序之间的合同;它们同意将平台用于数据传输。

在扫描之前，驱动程序必须使用平板扫描仪项目上的 WIA 属性作为要应用于扫描仪的平板部分的设置。 要求 WIA 应用程序始终信任 WIA 驱动程序返回的数据的标头。 例如，如果扫描程序确定它无法扫描指定宽度的图像，并因此将该值舍入到它可以扫描的宽度，则驱动程序应使用修改的宽度信息更新图像标头。 此更新可确保应用程序可使用正确的信息。 WIA 驱动程序应尝试用从设备返回的实际信息更新 WIA 属性。

### <a name="advanced-scanning-for-flatbed-scanners"></a>平板扫描仪的高级扫描

通过手动配置或自动使用 [WIA 分段筛选器](wia-segmentation-filter.md)，可以从平板进行多区域扫描。 请注意，分段筛选器与应用程序之间的不同之处在于它不会。 为分段筛选器描述的相同过程可以由应用程序直接运行，以创建新扫描区域的子项。

 

