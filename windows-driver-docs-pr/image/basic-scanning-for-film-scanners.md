---
title: 底片扫描仪的基本扫描
description: 底片扫描仪的基本扫描
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 74a0adc53db2ce78f7f64a2585046b09390f4d02
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96836437"
---
# <a name="basic-scanning-for-film-scanners"></a>底片扫描仪的基本扫描





WIA 应用程序枚举 "扫描程序" 项树中的顶级项，以确定扫描程序支持的功能。 然后，应用程序使用顶层项作为扫描源。 例如，平板扫描仪项用于从平板扫描，而送纸器项用于从文档送纸器进行扫描。

胶片项的编程和扫描行为与小小项的行为几乎相同。

应用程序通常会在计划扫描仪的胶卷项时执行以下操作，但不一定按以下顺序执行：

-   枚举顶级 WIA 项，搜索标有 **WiaItemTypeProgrammableDataSource** item 标志的 wia 项和 wia 类别胶卷的 [**wia \_ IPA \_ 项 \_ 类别**](./wia-ipa-item-category.md) 设置 \_ \_ 。

-   阅读 " [**WIA \_ IPS \_ 胶片 \_ 扫描 \_ 模式**](./wia-ips-film-scan-mode.md) " 的有效值以检查电影扫描设置。 此设置将指示正则图像或负图像 (即，照片消极) 扫描支持。

-   通过设置 "WIA \_ IPS \_ 胶片 \_ 扫描模式" 属性，选择正面或反面光源 \_ 。

-   如果需要，请阅读扫描仪灯的当前设置，并根据需要使用 [**WIA \_ IPS \_ 灯泡**](./wia-ips-lamp.md) 属性)  (。

-   读取 [**wia \_ IPA \_ TYMED**](./wia-ipa-tymed.md) 和 [**wia \_ IPA \_ 格式**](./wia-ipa-format.md)的有效值。

-   通过设置 WIA \_ IPA format 属性来选择数据的最终格式 \_ 。

-   选择图像设置，如 [**wia \_ IPA \_ DEPTH**](./wia-ipa-depth.md)、 [**wia \_ IPA \_ DATATYPE**](./wia-ipa-datatype.md)和 [**wia \_ IPA \_ 位 \_ / \_ 通道**](./wia-ipa-bits-per-channel.md)。

-   通过设置 WIA \_ IPA TYMED 属性，选择单个或多页 (（如果支持）) 文件传输 \_ 。

-   枚举子项以查找现有的帧。

-   阅读 " [**WIA \_ ip \_ 支持 \_ 子 \_ 项目 \_ 创建**](./wia-ips-supports-child-item-creation.md) 项目"，以确定扫描程序是否支持创建新帧。

-   根据框架创建支持) ，调整现有胶卷项帧或创建新框架 (。

-   \_ \_ \_ \_ \_ 若要确定胶卷扫描器项是否支持特殊的文件夹获取功能，请参阅 WIA ip 支持子项目创建属性。

-   执行下列操作之一：
    -   使用 WIA 胶片扫描器项传输数据 (不能使用文件夹获取功能) 。 完整胶片扫描区域将作为单个图像返回。
    -   使用 WIA 胶片扫描器项 (传输数据) 使用文件夹获取功能。 只有 WIA 胶片扫描器子项 (即，框架) 会传输到应用程序。
    -   导航到每个帧项并传输该 WIA 项。

当驱动程序使用扫描程序的胶片扫描单元扫描时，驱动程序通常会执行以下操作：

1.  调用 [**IWiaMiniDrv：:D rvvalidateitemproperties**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties) 和 [**IWiaMiniDrv：:d rvreaditemproperties**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvreaditemproperties)。 WIA 驱动程序应在应用程序的属性设置阶段验证所有属性设置。

2.  调用 [**IWiaMiniDrv：:D rvwriteitemproperties**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvwriteitemproperties)。 传入的 WIA 项上下文属于胶片扫描器项或胶卷扫描项帧，以便驱动程序知道应用程序打算使用扫描仪的电影扫描单元进行扫描。 某些扫描仪使用其 flatbeds 进行胶片扫描。 必须根据 WIA \_ IPS \_ 胶片 \_ 扫描 \_ 模式属性) 和区更改以进行胶片扫描，对扫描仪进行正确的照明 (配置。

3.  调用 [**IWiaMiniDrv：:D rvacquireitemdata**](/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)。 传入的 WIA 项上下文属于胶片扫描器项或胶卷扫描项帧。 驱动程序可以轻松确定应用程序要使用胶片扫描单元进行扫描。

4.  使用当前胶卷项属性对设备进行编程，并使用当前电影扫描单元进行扫描 (包括) 的任何子框架属性。 如果 WIA 驱动程序未处于胶片扫描模式，则它会尝试切换到此模式以进行扫描。 应用程序只能在反面和正光源之间切换。 使用胶片扫描器项进行扫描是指应用程序与驱动程序之间的合同;他们同意，扫描程序的胶片扫描功能将用于数据传输。

位于胶片扫描器项上的 WIA 属性应该由驱动程序使用，作为在扫描前应用于扫描程序的胶片扫描部分的设置。 要求 WIA 应用程序始终信任 WIA 驱动程序返回的数据的标头。 例如，扫描程序已确定它无法扫描指定的图像宽度，需要向上舍入值。 驱动程序应更新包含更新的宽度信息的图像标头，以便应用程序具有正确的数据。 WIA 驱动程序应始终用从设备返回的实际数据信息更新 WIA 属性集。

 

