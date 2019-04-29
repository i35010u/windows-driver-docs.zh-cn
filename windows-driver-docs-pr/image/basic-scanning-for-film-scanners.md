---
title: 底片扫描仪的基本扫描
description: 底片扫描仪的基本扫描
ms.assetid: ca25c14d-120e-4e53-9d57-ba5663536bae
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c055b8743eeb97b505a6f2daf8efc79232580dd8
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63373330"
---
# <a name="basic-scanning-for-film-scanners"></a>底片扫描仪的基本扫描





WIA 应用程序枚举扫描程序项树来确定扫描程序的受支持的功能中的顶级项。 然后，应用程序使用的顶级项作为扫描的源。 例如，平板扫描仪项用于平板、 从扫描和送纸器项用于从文档送纸器扫描。

编程和扫描的电影胶片项行为是与平板项几乎相同。

当程序扫描程序的电影胶片项，但不是一定按此顺序，应用程序通常将执行以下操作：

-   枚举顶级 WIA 项，搜索标有的 WIA 项**WiaItemTypeProgrammableDataSource**项标志并[ **WIA\_IPA\_项\_类别**](https://msdn.microsoft.com/library/windows/hardware/ff551581)设置的 WIA\_类别\_电影胶片。

-   读取的有效值[ **WIA\_IPS\_电影\_扫描\_模式**](https://msdn.microsoft.com/library/windows/hardware/ff552598)检查电影扫描设置。 此设置将指示正映像或底片图像 （即，是摄影底片） 扫描的支持。

-   通过设置 WIA 选择光源正值或负值\_IPS\_电影\_扫描\_模式属性。

-   读取扫描程序 lamp 的当前设置并打开灯泡，根据需要使用[ **WIA\_IPS\_LAMP** ](https://msdn.microsoft.com/library/windows/hardware/ff552603)属性 （如果支持）。

-   读取的有效值[ **WIA\_IPA\_TYMED** ](https://msdn.microsoft.com/library/windows/hardware/ff551656)并[ **WIA\_IPA\_格式**](https://msdn.microsoft.com/library/windows/hardware/ff551553).

-   选择数据的最终格式通过设置 WIA\_IPA\_格式属性。

-   选择映像设置，如[ **WIA\_IPA\_深度**](https://msdn.microsoft.com/library/windows/hardware/ff551546)， [ **WIA\_IPA\_DATATYPE** ](https://msdn.microsoft.com/library/windows/hardware/ff551543)，并[ **WIA\_IPA\_位\_每\_通道**](https://msdn.microsoft.com/library/windows/hardware/ff551526)。

-   选择一个或多页 （如果支持） 文件传输，通过设置 WIA\_IPA\_TYMED 属性。

-   枚举子项以查找现有的帧。

-   读取[ **WIA\_IPS\_支持\_子\_项\_创建**](https://msdn.microsoft.com/library/windows/hardware/ff552653)项来确定扫描程序是否支持创建新帧。

-   调整现有电影项帧或创建新帧 （具体取决于帧创建支持）。

-   读取 WIA\_IPS\_支持\_子\_项\_创建属性来确定电影扫描程序项是否支持特殊文件夹获取功能。

-   执行以下操作之一：
    -   将数据传输 （不是通过使用文件夹采集功能） 使用 WIA 电影扫描程序项。 完整扫描区域的电影将返回为单个映像。
    -   将数据传输 （通过使用文件夹采集功能） 使用 WIA 电影扫描程序项。 仅 WIA 电影扫描程序子项目 （即，帧） 传输到应用程序。
    -   导航到每个帧项并传输 WIA 该项。

使用扫描程序的电影胶片扫描单元进行扫描时，该驱动程序通常执行以下操作：

1.  调用[ **IWiaMiniDrv::drvValidateItemProperties** ](https://msdn.microsoft.com/library/windows/hardware/ff545017)并[ **IWiaMiniDrv::drvReadItemProperties**](https://msdn.microsoft.com/library/windows/hardware/ff545005)。 WIA 驱动程序应在应用程序的属性设置阶段过程中验证任何属性设置。

2.  调用[ **IWiaMiniDrv::drvWriteItemProperties**](https://msdn.microsoft.com/library/windows/hardware/ff545020)。 传入的 WIA 项上下文所属到电影扫描程序项或电影，以便让驱动程序知道应用程序想要使用扫描程序的电影胶片扫描单元扫描正在扫描项目框架。 某些扫描仪用于其 flatbeds 电影扫描。 扫描程序必须配置为正确的照明 (基于 WIA\_IPS\_电影\_扫描\_模式属性) 和盘区更改为电影胶片扫描。

3.  调用[ **IWiaMiniDrv::drvAcquireItemData**](https://msdn.microsoft.com/library/windows/hardware/ff543956)。 传入的 WIA 项上下文所属到电影扫描程序项或电影正在扫描项目框架。 该驱动程序可以轻松地确定应用程序想要使用扫描单元电影扫描。

4.  对设备和扫描从电影扫描单元使用当前电影项目属性 （包括任何子帧属性）。 如果 WIA 驱动程序不是电影胶片扫描模式，它将尝试切换到扫描此模式。 应用程序可能仅切换负数和正数 light。 使用胶片扫描程序项要扫描是应用程序和驱动程序; 之间的协定用户同意电影扫描扫描程序的功能将用于数据传输。

位于电影扫描程序项的 WIA 属性应用作由驱动程序设置要应用于电影扫描在扫描之前的扫描程序的一部分。 WIA 应用程序需要始终信任 WIA 驱动程序返回的数据的标头。 例如，扫描程序已确定其无法扫描指定的图像宽度和需要值向上舍入。 该驱动程序应使用的更新的宽度信息更新映像标头，以便应用程序具有正确的数据。 WIA 驱动程序应始终更新 WIA 属性将设置从设备返回的实际数据信息。

 

 




