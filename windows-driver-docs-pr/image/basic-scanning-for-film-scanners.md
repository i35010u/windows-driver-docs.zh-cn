---
title: 底片扫描仪的基本扫描
description: 底片扫描仪的基本扫描
ms.assetid: ca25c14d-120e-4e53-9d57-ba5663536bae
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: beaf60e61309798c8810a1e0afd07aea39578d75
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840891"
---
# <a name="basic-scanning-for-film-scanners"></a>底片扫描仪的基本扫描





WIA 应用程序枚举 "扫描程序" 项树中的顶级项，以确定扫描程序支持的功能。 然后，应用程序使用顶层项作为扫描源。 例如，平板扫描仪项用于从平板扫描，而送纸器项用于从文档送纸器进行扫描。

胶片项的编程和扫描行为与小小项的行为几乎相同。

应用程序通常会在计划扫描仪的胶卷项时执行以下操作，但不一定按以下顺序执行：

-   枚举顶级 WIA 项，搜索标有**WiaItemTypeProgrammableDataSource** item 标志和[**wia\_IPA\_item\_类别**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-item-category)设置为\_wia 的 wia 项\_胶片。

-   读取[**WIA\_IPS\_电影\_扫描\_模式**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-film-scan-mode)的有效值以检查电影扫描设置。 此设置将指示正图像或负片图像（即照相底片）扫描支持。

-   通过设置 WIA\_IP\_胶卷\_SCAN\_模式属性，选择正或负光源。

-   如果需要，请阅读扫描仪灯的当前设置，并使用[**WIA\_IPS\_灯泡**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-lamp)属性（如果支持）来打开灯泡。

-   读取[**wia\_IPA\_TYMED**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-tymed)和[**WIA\_IPA\_格式**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-format)的有效值。

-   通过设置 WIA\_IPA\_FORMAT 属性来选择数据的最终格式。

-   选择图像设置，例如[**WIA\_IPA\_DEPTH**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-depth)、 [**wia\_IPA\_数据类型**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-datatype)和[**WIA\_每\_通道 IPA\_位数**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ipa-bits-per-channel)。

-   通过设置 WIA\_IPA\_TYMED 属性来选择单个或多页（如果支持）文件传输。

-   枚举子项以查找现有的帧。

-   阅读[**WIA\_IPS\_支持\_子\_项\_创建**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-ips-supports-child-item-creation)项，以确定扫描程序是否支持创建新框架。

-   调整现有胶卷项帧或创建新帧（具体取决于创建框架的支持）。

-   阅读 WIA\_IPS\_支持\_子\_项\_创建属性来确定胶卷扫描器项是否支持特殊的文件夹获取功能。

-   执行下列操作之一：
    -   使用 WIA 胶片扫描器项（而不是使用文件夹获取功能）传输数据。 完整胶片扫描区域将作为单个图像返回。
    -   使用 WIA 胶片扫描器项（通过使用文件夹获取功能）传输数据。 只有 WIA 胶片扫描器子项目（即帧）会传输到应用程序。
    -   导航到每个帧项并传输该 WIA 项。

当驱动程序使用扫描程序的胶片扫描单元扫描时，驱动程序通常会执行以下操作：

1.  调用[**IWiaMiniDrv：:D rvvalidateitemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvvalidateitemproperties)和[**IWiaMiniDrv：:d rvreaditemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvreaditemproperties)。 WIA 驱动程序应在应用程序的属性设置阶段验证所有属性设置。

2.  调用[**IWiaMiniDrv：:D rvwriteitemproperties**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvwriteitemproperties)。 传入的 WIA 项上下文属于胶片扫描器项或胶卷扫描项帧，以便驱动程序知道应用程序打算使用扫描仪的电影扫描单元进行扫描。 某些扫描仪使用其 flatbeds 进行胶片扫描。 必须根据 WIA\_IP\_胶卷\_SCAN\_模式属性）和区更改进行胶片扫描，来配置扫描仪的照明度。

3.  调用[**IWiaMiniDrv：:D rvacquireitemdata**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamindr_lh/nf-wiamindr_lh-iwiaminidrv-drvacquireitemdata)。 传入的 WIA 项上下文属于胶片扫描器项或胶卷扫描项帧。 驱动程序可以轻松确定应用程序要使用胶片扫描单元进行扫描。

4.  使用当前胶卷项属性（包括任何子框架属性）对设备进行编程，并使用当前电影扫描单元进行扫描。 如果 WIA 驱动程序未处于胶片扫描模式，则它会尝试切换到此模式以进行扫描。 应用程序只能在反面和正光源之间切换。 使用胶片扫描器项进行扫描是指应用程序与驱动程序之间的合同;他们同意，扫描程序的胶片扫描功能将用于数据传输。

位于胶片扫描器项上的 WIA 属性应该由驱动程序使用，作为在扫描前应用于扫描程序的胶片扫描部分的设置。 要求 WIA 应用程序始终信任 WIA 驱动程序返回的数据的标头。 例如，扫描程序已确定它无法扫描指定的图像宽度，需要向上舍入值。 驱动程序应更新包含更新的宽度信息的图像标头，以便应用程序具有正确的数据。 WIA 驱动程序应始终用从设备返回的实际数据信息更新 WIA 属性集。

 

 




