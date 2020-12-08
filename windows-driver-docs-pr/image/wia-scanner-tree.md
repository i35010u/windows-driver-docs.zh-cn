---
title: WIA 扫描器树
description: WIA 扫描器树提供有关根项 (扫描器) 的信息，以及由照相机和扫描仪通用的属性组成的每个子项的信息。
ms.date: 07/06/2020
ms.localizationpriority: medium
ms.openlocfilehash: 242cd6e5f2f5213a45b2f24dc539a483ceee71aa
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826425"
---
# <a name="wia-scanner-tree"></a>WIA 扫描器树

下图显示了一个扫描仪和它生成的映像。

![说明扫描仪和它生成的映像的关系图](images/art-scanner.png)

下图显示了 Microsoft Windows Me 或 Windows XP 扫描器，或在 Windows Vista 上没有文档送纸器、双面打印器或胶片扫描器的扫描仪。

WIA 将上图中显示的扫描仪及其图像表示为项树，如下图所示。

![说明 wia 如何将扫描仪及其图像表示为项树的关系图](images/art-4.png)

根项是扫描程序本身，它包含 (照相机和扫描仪) 的通用设备属性和扫描仪特定的设备属性。 同样，每个子项都包含照相机和扫描仪项所共有的属性，以及特定于扫描程序项的属性。

通过 WIA 服务，应用程序可以从扫描仪项请求以下内容：

- 查询扫描程序功能

- 设置扫描仪设备属性

- 请求数据传输

在 Windows Me 和 Windows XP 中，直接位于根项的下方，典型的 scanner 对象具有单个项，即 scanner 项，表示设备的数据收集功能。 应用程序通过设置扫描程序项的属性来设置扫描。 当应用程序通过 WIA 服务从项请求数据时执行扫描。

在 Windows Me 和 Windows XP 中，应用程序通常需要平板扫描仪，其中包括具有自动文档送纸送 (ADFs) 的扫描程序，这些扫描程序由两个项目（一个根项和一个子节点）表示。 所有数据传输都是从子项目中执行的。 驱动程序可以选择创建其他项以供其专用，并且可以将这些项设为传输功能。  (，请在对 [**wiasCreateChildAppItem**](/windows-hardware/drivers/ddi/wiamdef/nf-wiamdef-wiascreatechildappitem)的调用中设置项类型标志的 WiaItemTypeTransfer 位。 此常量记录在 Microsoft Windows SDK 文档中。 ) 不过，应用程序通常不知道这些私有项，也不知道如何处理它们。 对于带有 ADF 的扫描仪，在 Windows Me 或 Windows XP 中，可以通过将 WIA \_ DPS \_ 文档 \_ 处理 \_ *XXX* 属性添加到扫描仪的根项而不是扫描程序的子项来公开和控制 adf 功能。 有关这些属性的详细信息，请参阅 [WIA properties](./wia-properties.md)。 有关 Windows Vista 中带有 ADF 的扫描仪的信息，请参阅 [WIA 进纸器扫描仪](wia-feeder-scanners.md)。

如果设备有平台和 ADF，并且可以进行双工扫描，在 Windows Me 或 Windows XP 中，驱动程序会将 " [**WIA \_ DPS \_ 文档 \_ 处理 \_ 功能**](./wia-dps-document-handling-capabilities.md) " 属性报告为 (源 &#x7c; 平面 &#x7c; DUP) 。

请确保正确设置了 [**WIA \_ DPS \_ 文档 \_ 处理 \_**](./wia-dps-document-handling-select.md) 的有效值。 请注意，在单个扫描作业中扫描的所有文档都将存在于项树中的单个子项中。 有关使用 ADF 和 Windows Vista 上的双面打印器的信息，请参阅 [WIA 进纸器扫描仪](wia-feeder-scanners.md)。

例如，假设应用程序要从 ADF 执行三页的双工扫描。 若要完成此操作，应用程序会将 "WIA \_ dps \_ 文档 \_ 处理" \_ 选择属性设置为 (送纸器 &#x7c; 双工) ，并将 " [**WIA \_ DPS \_ 页面**](./wia-dps-pages.md) " 属性设置为3。 如果应用程序首先要扫描页面正面，则应将 "WIA \_ DPS \_ 文档 \_ 处理" \_ 选择属性设置为 " (进纸器 &#x7c; 双工 &#x7c; \_ 第一) 。 完成此操作后，应用程序应导航到从中请求数据传输的子项。 微型驱动程序会将 ADF 中第一页的正面报告为第1页，该页面的背面为第2页，而 ADF 中第二页的正面为页面3。

请记住，如果设备有 ADF，则必须支持 ADF 属性。
