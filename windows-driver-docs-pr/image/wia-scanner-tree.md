---
title: WIA 扫描仪树
description: WIA 扫描仪树
ms.assetid: bd1452b9-1926-4dd6-b94c-e44f07573266
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: dcaa5c3e781f9306a4939f7c5e32c272c972ba98
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72840669"
---
# <a name="wia-scanner-tree"></a>WIA 扫描仪树





下图显示了一个扫描仪和它生成的映像。

![说明扫描仪和它生成的映像的关系图](images/art-scanner.png)

下图显示了 Microsoft Windows Me 或 Windows XP 扫描器，或在 Windows Vista 上没有文档送纸器、双面打印器或胶片扫描器的扫描仪。

WIA 将上图中显示的扫描仪及其图像表示为项树，如下图所示。

![说明 wia 如何将扫描仪及其图像表示为项树的关系图](images/art-4.png)

根项是扫描程序本身，由通用设备属性（照相机和扫描仪通用的属性）和扫描程序特定的设备属性组成。 同样，每个子项都包含照相机和扫描仪项所共有的属性，以及特定于扫描程序项的属性。

通过 WIA 服务，应用程序可以从扫描仪项请求以下内容：

-   查询扫描程序功能。

-   设置扫描程序设备属性。

-   请求数据传输。

在 Windows Me 和 Windows XP 中，直接位于根项的下方，典型的 scanner 对象具有单个项，即 scanner 项，表示设备的数据收集功能。 应用程序通过设置扫描程序项的属性来设置扫描。 当应用程序通过 WIA 服务从项请求数据时执行扫描。

在 Windows Me 和 Windows XP 中，应用程序通常会期望平板扫描仪（包括带有自动文档送纸程序（ADFs）的扫描仪）由两个项（根项和一个子）表示。 所有数据传输都是从子项目中执行的。 驱动程序可以选择创建其他项以供其专用，并且可以将这些项设为传输功能。 （为此，请在对[**wiasCreateChildAppItem**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatechildappitem)的调用中设置项类型标志的 WiaItemTypeTransfer 位。 此常量记录在 Microsoft Windows SDK 文档中。）但是，应用程序通常不知道这些私有项，也不知道如何处理它们。 对于带有 ADF 的扫描仪，在 Windows Me 或 Windows XP 中，通过将 WIA\_DPS\_文档\_处理\_*XXX*属性添加到扫描仪的根项（而不是扫描程序的子项目。 有关这些属性的详细信息，请参阅[WIA properties](https://docs.microsoft.com/windows-hardware/drivers/image/wia-properties)。 有关 Windows Vista 中带有 ADF 的扫描仪的信息，请参阅[WIA 进纸器扫描仪](wia-feeder-scanners.md)。

如果设备有平台和 ADF，并且可以进行双工扫描，在 Windows Me 或 Windows XP 中，驱动程序会将[**WIA\_DPS\_文档\_处理\_功能**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-capabilities)属性作为源 |平面 |DUP）。 请确保正确设置了[**WIA\_DPS\_文档\_\_处理**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-document-handling-select)的有效值。 请注意，在单个扫描作业中扫描的所有文档都将存在于项树中的单个子项中。 有关使用 ADF 和 Windows Vista 上的双面打印器的信息，请参阅[WIA 进纸器扫描仪](wia-feeder-scanners.md)。

例如，假设应用程序要从 ADF 执行三页的双工扫描。 若要完成此操作，应用程序会将 WIA\_DPS\_文档\_处理设置\_选择属性设置为（进纸器 |双工），并将[**WIA\_DPS\_PAGES**](https://docs.microsoft.com/windows-hardware/drivers/image/wia-dps-pages)属性设置为3。 如果应用程序首先要扫描页面正面，则应将 WIA\_DPS\_文档\_处理\_选择属性设置为（进纸器 |双工 |前面\_第一个）。 完成此操作后，应用程序应导航到从中请求数据传输的子项。 微型驱动程序会将 ADF 中第一页的正面报告为第1页，该页面的背面为第2页，而 ADF 中第二页的正面为页面3。

请记住，如果设备有 ADF，则必须支持 ADF 属性。

 

 




