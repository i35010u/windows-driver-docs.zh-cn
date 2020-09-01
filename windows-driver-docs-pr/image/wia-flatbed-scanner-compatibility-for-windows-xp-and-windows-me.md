---
title: Windows XP 和 Windows Me 的 WIA 平板扫描仪兼容性
description: Windows XP 和 Windows Me 的 WIA 平板扫描仪兼容性
ms.assetid: fc3424fa-3898-4f6a-a611-f81d97db8b1d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: c5e40c08221c408b5e85175aa4948b085f754e4d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89191493"
---
# <a name="wia-flatbed-scanner-compatibility-for-windows-xp-and-windows-me"></a>Windows XP 和 Windows Me 的 WIA 平板扫描仪兼容性





Windows Vista WIA 项树会导致为 Windows XP 和 Windows Me 编写的应用程序中出现一些兼容性问题。

为了简化 Windows Vista WIA 驱动程序和应用程序以及旧版 WIA 驱动程序和应用程序之间的兼容性问题，Windows Vista 具有内部兼容性层。 此兼容性层允许将 Windows XP (和 Windows Me 分别用于 Windows Vista 驱动程序和应用程序) 驱动程序和应用程序。 在 Windows Vista 上，此转换过程对驱动程序和应用程序都是透明的。 有关此兼容性层的详细信息，请参阅 [WIA 兼容性层](wia-compatibility-layer.md)。

但是，windows XP 或 Windows Me 上 Windows Vista 驱动程序和应用程序的兼容性更复杂。 为在这些旧操作系统上存在的 WIA 版本编写的应用程序遵循一组不同的规则和假设。 Windows XP 和 Windows Me 中的 WIA 扫描器项树将扫描仪的功能合并到项树中的单个项。 根项控制该项的传输行为。 例如，扫描器使用第一个子项作为可编程数据源，根项属性 [**WIA \_ DPS \_ 文档 \_ 处理 \_ 选择**](./wia-dps-document-handling-select.md) " \_ \_ 在 Windows Vista 中选择 (称为 WIA ip 文档 \_ 处理 \_ "，) 在平板扫描和进纸器扫描之间切换。

此项重载方法要求应用程序为重要的 WIA 项跟踪所需的 WIA 属性，以帮助对扫描仪的功能分类。 如果扫描程序 \_ \_ \_ \_ 的根项上存在 WIA DPS 文档处理选择属性，则应用程序假定扫描程序支持从文档送纸器进行扫描。 如果将此属性设置为 "平板"，则应用程序会假定扫描仪还支持平板影印扫描。 因此，较旧的 WIA 应用程序将导航到新的 WIA 扫描器项树的根目录，并且找不到任何告知其设备功能的属性。

**注意**   如果实现了其他扫描数据源，则平板扫描仪项必须是 WIA 项树中的第一个子项目。 此位置可确保能够操作基本平板扫描仪的 Windows XP 和 Windows Me 应用程序将自动找到设备的平板扫描功能。 某些应用程序会导航到作为唯一子项的第一个子项目，并假定它是扫描仪的平台或送纸器。 将带有平台扫描仪项的扫描仪项树实现为第一个子项会阻止许多向后兼容性问题。

 

有关兼容性的详细信息，请参阅 [WIA 项目属性和位置更改](wia-item-property-and-location-changes.md)。

 

