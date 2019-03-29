---
title: WIA 扫描仪树
description: WIA 扫描仪树
ms.assetid: bd1452b9-1926-4dd6-b94c-e44f07573266
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dec5bb51ed96c7f25369bb5f97389dc37bfc69de
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566096"
---
# <a name="wia-scanner-tree"></a>WIA 扫描仪树





下图显示了扫描仪和它生成一个图像。

![说明扫描仪和它生成一个图像的关系图](images/art-scanner.png)

下图显示了 Microsoft Windows Me 或 Windows XP 的扫描程序或扫描程序在 Windows Vista 上该扫描程序是否提供任何文档送纸器、 双面打印器或电影扫描程序。

WIA 表示扫描程序和其图像在上图中显示为项树中，如图所示。

![说明如何 wia 表示扫描程序和其图像作为项树的关系图](images/art-4.png)

根项，它是扫描程序本身，包括通用设备属性 （照相机和扫描仪共有的属性） 和特定于扫描程序的设备属性。 同样，每个子项包括照相机和扫描仪项通用的属性，以及特定于扫描程序项的属性。

通过 WIA 的服务，应用程序可以从扫描程序项请求以下：

-   查询扫描程序功能。

-   设置扫描程序的设备属性。

-   请求数据传输。

在 Windows Me 和 Windows XP，正下方的根项目中，典型的扫描程序对象具有单个项，扫描程序项，它表示的设备的数据收集功能。 通过设置扫描程序项目的属性，应用程序设置一次扫描。 应用程序请求数据时，通过 WIA 的服务，从项时，将执行扫描。

在 Windows Me 和 Windows XP 中，应用程序通常预期平板扫描仪，包括那些使用自动文档送纸器 (ADFs)，通过两个项-根项目和单个子来表示。 从子项目执行所有的数据量。 驱动程序可以选择创建供其专用的其他项，而这些项可以成为支持传输的。 (为此，请在调用中设置项类型标志的 WiaItemTypeTransfer 位[ **wiasCreateChildAppItem**](https://msdn.microsoft.com/library/windows/hardware/ff549156)。 此常量中介绍了 Microsoft Windows SDK 文档。）但是，应用程序通常不了解的关于这些专用的项，并且不知道如何对其进行处理。 ADF 功能是使用 ADF，在 Windows Me 或 Windows XP 中，扫描程序公开并控制通过添加 WIA\_DPS\_文档\_处理\_*XXX*属性扫描程序的根项，而不是到扫描程序的子窗体项。 有关这些属性的详细信息，请参阅[WIA 属性](https://msdn.microsoft.com/library/windows/hardware/ff552739)。 有关使用 Windows Vista 中 ADF 扫描程序的信息，请参阅[WIA 送纸器扫描仪](wia-feeder-scanners.md)。

如果设备具有平板和 ADF 中，并且可以执行双工扫描，在 Windows Me 或 Windows XP 驱动程序将报告[ **WIA\_DPS\_文档\_处理\_功能**](https://msdn.microsoft.com/library/windows/hardware/ff551379)属性作为 (源 |平面 |DUP)。 请确保为有效值[ **WIA\_DPS\_文档\_处理\_选择**](https://msdn.microsoft.com/library/windows/hardware/ff551384)正确设置。 请注意项树中的单个子选项中将存在的单个扫描作业中已扫描的所有文档。 有关使用 ADF 扫描仪和双面打印器在 Windows Vista 上的信息，请参阅[WIA 送纸器扫描仪](wia-feeder-scanners.md)。

例如，假设应用程序想要从 ADF 执行双工扫描三个页面。 若要实现此目的，应用程序需要设置 WIA\_DPS\_文档\_处理\_选择属性 (送纸器 |双工），并将[ **WIA\_DPS\_页**](https://msdn.microsoft.com/library/windows/hardware/ff551414)属性设置为 3。 如果应用程序想要首先扫描前面的页面，它应设置 WIA\_DPS\_文档\_处理\_选择属性 (送纸器 |双工 |前\_第一个)。 此操作完成后，应用程序应导航到子项目，它将从其请求数据传输。 微型驱动程序会报告在 ADF 中为第 1 页、 第 2 页，为该页面后和在 ADF 中一样的第 3 页的第二页前面的第一页的前面。

请务必记住，是否该设备已 ADF，它必须支持 ADF 属性。

 

 




