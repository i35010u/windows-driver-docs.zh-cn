---
title: WIA 平板扫描仪兼容性的 Windows XP 和 Windows Me
description: WIA 平板扫描仪兼容性的 Windows XP 和 Windows Me
ms.assetid: fc3424fa-3898-4f6a-a611-f81d97db8b1d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4665903ce1cc4e878167bfc801ce702b2ccbe8d
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56524512"
---
# <a name="wia-flatbed-scanner-compatibility-for-windows-xp-and-windows-me"></a>WIA 平板扫描仪兼容性的 Windows XP 和 Windows Me





Windows Vista WIA 项树针对 Windows XP 和 Windows me.编写的应用程序中导致某些兼容性问题

若要简化 Windows Vista WIA 驱动程序和应用程序和旧 WIA 驱动程序和应用程序之间的兼容性问题，Windows Vista 有内部兼容性层。 此兼容性层将允许您分别与 Windows Vista 驱动程序和应用程序，使用 Windows XP （和 Windows Me） 驱动程序和应用程序。 在 Windows Vista 中，此转换过程是透明的驱动程序和应用程序。 有关此兼容性层的详细信息，请参阅[WIA 兼容性层](wia-compatibility-layer.md)。

但是，Windows Vista 驱动程序和 Windows XP 或 Windows Me 上的应用程序兼容性是更复杂。 这些旧的操作系统存在的 WIA 的版本编写的应用程序遵循一组不同的规则和假设。 WIA 扫描程序在 Windows XP 和 Windows Me 合并到项目树中的单个项上的扫描程序的功能项树。 根项控制该子项的传输行为。 例如，扫描程序使用第一个子项目作为可编程数据源和根项属性[ **WIA\_DPS\_文档\_处理\_选择**](https://msdn.microsoft.com/library/windows/hardware/ff551384) (称为 WIA\_IPS\_文档\_处理\_选择 Windows Vista 中) 平板扫描和送纸器扫描之间进行切换。

此项重载方法要求应用程序来跟踪的重要 WIA 各项以帮助进行分类的扫描仪功能的必需的 WIA 属性。 如果 WIA\_DPS\_文档\_处理\_扫描程序的根项上存在选择属性，该应用程序假设在扫描仪支持从文档送纸器扫描。 如果此属性设置为平板，该应用程序假设扫描程序还支持平板辊扫描。 因此，较旧 WIA 应用程序将导航到新的 WIA 扫描程序项树的根和将找不到任何属性，告诉他们设备的功能。

**请注意**  平板扫描仪项必须是 WIA 项树中的第一个子项目，如果实现了其他扫描的数据源。 此位置可确保 Windows XP 和 Windows Me 的应用程序能够运行基本平板扫描仪将自动查找平板扫描你的设备的功能。 某些应用程序导航到第一个子项目，用于将唯一的子项目，并假定它是平板或扫描程序的送纸器。 实现通过平板扫描仪项目作为第一个子项目的扫描程序项树将防止出现许多向后兼容性问题。

 

有关兼容性的详细信息，请参阅[WIA 项属性和位置更改](wia-item-property-and-location-changes.md)。

 

 




