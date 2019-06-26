---
title: 平板扫描仪的基本扫描
description: 平板扫描仪的基本扫描
ms.assetid: a1100a8d-752a-4109-b1dc-cf7c4bf5a100
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f3d82c0110317438abdbd1c68abab68e434e4b4a
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67366754"
---
# <a name="basic-scanning-for-flatbed-scanners"></a>平板扫描仪的基本扫描





WIA 应用程序枚举的根项目，然后扫描程序项树来确定扫描程序的受支持的功能中的顶级子项目。 然后，应用程序使用此子项目作为扫描的源。 例如，平板扫描仪项用于扫描从平板、 送纸器项用于实现文档送纸器，从扫描等。

Windows Vista 中的平板项的编程和扫描行为等同于重载系统，由 Windows XP 和 Windows me 一起提供。 此重载系统程序通过将所有 WIA 特性标志放在其上的项树中的第一个子项目。

当程序扫描程序的平板、 但不是一定按此顺序，应用程序通常将执行以下操作：

-   枚举顶级 WIA 项并查找标记有项， **WiaItemTypeProgrammableDataSource**项标志且[ **WIA\_IPA\_项\_类别**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-category)属性设置为 WIA\_类别\_平板。

-   读取的有效值[ **WIA\_IPA\_TYMED** ](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-tymed)并[ **WIA\_IPA\_格式**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-format)属性。

-   选择任一内存传输或文件传输类型通过设置 WIA\_IPA\_TYMED 属性。 有关可用的传输类型的详细信息，请参阅[数据传输](data-transfers.md)。 有关**IStream**-基于传输，WIA\_IPA\_TYMED 默认设置为 TYMED\_文件，不应更改。

-   选择数据的最终格式通过设置 WIA\_IPA\_格式属性。

-   选择映像设置，如[ **WIA\_IPA\_深度**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-depth)并[ **WIA\_IPA\_DATATYPE**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-datatype).

-   使用此 WIA 项将数据传输。

使用扫描程序的平板扫描时，该驱动程序通常将执行以下操作：

1.  调用[ **IWiaMiniDrv::drvValidateItemProperties** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)并[ **IWiaMiniDrv::drvReadItemProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvreaditemproperties)。 WIA 驱动程序应在应用程序的属性设置阶段过程中验证属性的任何设置。

2.  调用[ **IWiaMiniDrv::drvWriteItemProperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvwriteitemproperties)。 传入的 WIA 项上下文属于平板扫描仪项，以便让驱动程序知道应用程序想要使用扫描程序的平板扫描。

3.  调用[ **IWiaMiniDrv::drvAcquireItemData**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)。 传入的 WIA 项上下文属于平板扫描仪项，因此驱动程序可以轻松地确定应用程序想要使用平板辊扫描。

4.  程序设备，并从平板、 使用的当前平板项属性的扫描。 如果 WIA 驱动程序不在平板扫描模式下，它应尝试切换到扫描此模式。 没有特殊的设置应用程序切换为使用平板。 使用平板项要扫描是应用程序和驱动程序; 之间的协定用户同意平板时要使用的数据传输。

该驱动程序必须 WIA 属性上使用平板扫描仪项设置为要应用于的平板扫描仪扫描前一部分。 WIA 应用程序需要始终信任 WIA 驱动程序返回的数据的标头。 例如，如果扫描程序确定无法扫描指定的宽度的图像，并且，因此，将它可以扫描宽度值舍入，驱动程序应使用修改后的宽度信息更新的映像标头。 此更新可确保正确的信息可供该应用程序。 WIA 驱动程序应尝试更新 WIA 属性，但从设备返回的实际信息。

### <a name="advanced-scanning-for-flatbed-scanners"></a>高级扫描平板扫描仪

多区域从平板扫描可能是任一但手动配置或通过自动使用[WIA 分段的筛选器](wia-segmentation-filter.md)。 请注意，分段的筛选器与中它可以和不能执行的应用程序没有什么不同。 可以直接通过要创建新的扫描区域的子项目的应用程序运行相同的过程所述为分段的筛选器。

 

 




