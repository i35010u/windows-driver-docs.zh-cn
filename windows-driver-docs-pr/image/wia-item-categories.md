---
title: WIA 项类别
description: WIA 项类别
ms.assetid: b201e365-60d8-4c3b-a9cf-4bbaa318337f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a42aa3a5ddbe5ba30916fc12190a7d9bc18c7862
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63363049"
---
# <a name="wia-item-categories"></a>WIA 项类别





本主题适用于 Windows Vista 和更高版本。

必须支持 WIA 项树中的所有项[ **WIA\_IPA\_项\_类别**](https://msdn.microsoft.com/library/windows/hardware/ff551581)属性。 此属性标识项所属的功能类别。 类别设置确定 WIA 项标志和 WIA 的与项关联的属性的集。

WIA 定义以下项类别：

<a href="" id="wia-category-root"></a>WIA\_类别\_根  
*根项*WIA 扫描设备的树项中表示作为一个整体的设备。 如果设备包括平板、 ADF 或扫描函数的电影，则表示这些输入的源的项的是根项的子级。 如果设备包含存储，设备的存储层次结构中的最顶层文件夹项是根项的子级。 应用程序可以访问设备，包括状态、 标识和访问权限，通过 WIA 属性上的根项目实现的相关信息。 有关详细信息，请参阅中的根项属性的讨论[实现平板扫描仪项树](implementing-flatbed-scanner-item-trees.md)，[实现送纸器扫描程序项树](implementing-feeder-scanner-item-trees.md)，和[实现电影胶片扫描程序项树](implementing-film-scanner-item-trees.md)。

<a href="" id="wia-category-flatbed"></a>WIA\_类别\_平板  
一个*平板项*表示 （也称为扫描辊） 的扫描平板 WIA 扫描程序设备上。 使用扫描平板设备的 WIA 项树应包含根项的子级的平板项。 此外，如果 WIA 设备支持分段 (例如，通过[分段的筛选器](wia-segmentation-filter.md)) 或多区域扫描此平板项应具有子级，这两项也平板项，来表示单个扫描区域上平板。 子项目中，当存在时，应属于同一 WIA\_类别\_平板类别作为其父级，并且它们应支持相同的 WIA 属性 （并具有相同的初始属性值） 作为其父级-不同之处在于位置和子项目的范围仅限于它们所代表的扫描区域。 应用程序可以使用 WIA 驱动程序的分段的筛选器 （如果有） 来创建扫描区域或微型驱动程序可以自动检测并创建扫描区域本身。 应用程序可以访问设备的平板扫描通过 WIA 属性上平板 （或多个项目） 实现的函数。 有关详细信息，请参阅[实现平板扫描仪项树](implementing-flatbed-scanner-item-trees.md)。

<a href="" id="wia-category-feeder"></a>WIA\_类别\_送纸器  
一个*送纸器项*表示自动文档送纸器 (ADF) WIA 扫描程序设备上的。 (此项类别还可以表示送纸器不是完全自动和手动协助用户需要的但在这种情况下，WIA 微型驱动程序负责验证之前它将扫描的下一步的文档页具有高级通过送纸器页。）使用 ADF 设备应包括其 WIA 项树中的送纸器项。 送纸器项是根项的子级。 应用程序可以访问设备的 ADF 扫描通过 WIA 属性上送纸器项实现的函数。 有关详细信息，请参阅[实现送纸器扫描程序项树](implementing-feeder-scanner-item-trees.md)。

如果 ADF 可以执行双工扫描 （即，扫描的文档页两面），并它支持不同的控件设置用于扫描文档页的前端和后端方面，WIA 微型驱动程序应实现的送纸器前项和作为一个送纸器后的项送纸器项的子级。 应用程序可以访问 ADF 前面并重新扫描函数通过 WIA 属性上送纸器前项实现上送纸器, 备份项。 有关这两项的详细信息，请参阅以下类别说明。

<a href="" id="wia-category-feeder-front"></a>WIA\_类别\_送纸器\_前端  
一个*送纸器前项*表示用于扫描的文档中的页正面的 ADF 设置。 此项应实现为 ADF，可以执行双工扫描并支持不同的控件设置用于扫描文档页的前端和后端方面的扫描程序设备 WIA 微型驱动程序。 始终对文档页的双方使用相同的设置了 ADF 的设备不需要此项。 送纸器前项是送纸器项的子级。 应用程序可以访问 ADF 前面扫描通过 WIA 属性上送纸器前项实现的函数。 有关详细信息，请参阅[实现送纸器扫描程序项树](implementing-feeder-scanner-item-trees.md)。

<a href="" id="wia-category-feeder-back"></a>WIA\_类别\_送纸器\_返回  
一个*送纸器后项*表示用于扫描文档中页的后端的 ADF 设置。 此项应实现为 ADF，可以执行双工扫描并支持不同的控件设置用于扫描文档页的前端和后端方面的扫描程序设备 WIA 微型驱动程序。 始终对文档页的双方使用相同的设置了 ADF 的设备不需要此项。 送纸器后项是送纸器项的子级。 应用程序可以访问的 ADF 重新扫描通过 WIA 属性上送纸器后项实现的函数。 有关详细信息，请参阅[实现送纸器扫描程序项树](implementing-feeder-scanner-item-trees.md)。

<a href="" id="wia-category-film"></a>WIA\_CATEGORY\_FILM  
一个*电影项*表示电影扫描 WIA 扫描程序设备上的函数。 设备专用的电影扫描仪，或者是配备有透明度适配器 (TPA) 平板扫描仪应该包括其 WIA 项树中的一个或多个电影项目。 电影项是子级的根项，或另一个电影项。 是根项的子级的电影胶片项表示整个扫描图面，并且此电影项可能必须表示为单个电影帧对应的扫描的图面区域的电影胶片项的子级。 应用程序可以访问设备的电影胶片扫描通过 WIA 属性上电影胶片 （或多个项目） 实现的函数。 有关详细信息，请参阅[实现电影胶片扫描程序项树](implementing-film-scanner-item-trees.md)。

<a href="" id="wia-category-folder"></a>WIA\_类别\_文件夹  
一个*文件夹项*表示位于 WIA 扫描程序设备在内部存储中的文件夹。 文件夹项是子级或另一个文件夹项的根项。 如果文件夹的项具有子项，子级都已完成的文件项和文件夹项的组合。 在项目树中的最顶层文件夹项是根项的子级。 应用程序可以通过在文件夹项上实现的 WIA 属性访问的文件夹的内容和文件夹的相关信息。 有关详细信息，请参阅[WIA 扫描程序存储](wia-scanner-storage.md)。

<a href="" id="wia-category-finished-file"></a>WIA\_类别\_已完成\_文件  
一个*已完成的文件项*表示 WIA 扫描程序设备上的文件夹中存储的已完成的文件。 已完成的文件是不会更改其内容的文件。 此定义不包括其内容可能会动态变化，例如，如获取扫描程序和进程图像数据的文件。 已完成的文件项是文件夹项的子级。 应用程序可以通过在已完成的文件项上实现的 WIA 属性访问完成的文件和文件的相关信息。 有关详细信息，请参阅[WIA 扫描程序存储](wia-scanner-storage.md)。

<a href="" id="wia-category-auto"></a>WIA\_类别\_自动  
在 Windows 7 和更高版本，[自动项](auto-item.md)表示支持的 WIA 扫描程序设备的自动配置设置[自动配置扫描](auto-configured-scanning.md)。 此类设备可以配置自己的扫描设置而不是要求通过在桌面计算机上运行的 WIA 应用程序配置的设置。 例如，如果该设备，用户可以启动从设备扫描操作 (而不是从应用程序的用户界面) 和从设备中选择操作的输入的源，该应用程序可用于自动项卸载、 为设备，配置所选的输入的源的任务。 自动项是根项的子级。 一个包含自动项的 WIA 树还必须包含一个或多个以下： 平板项、 送纸器项或电影项。 应用程序可以通过实现和自动项上的根项目 WIA 属性访问设备自动配置扫描的功能。 有关详细信息，请参阅[WIA 属性支持的自动项](wia-properties-supported-by-an-auto-item.md)。

每个 WIA 项类别都有一组必需的 WIA 项标志和 WIA 属性类别中的项必须支持，以及另外，项可以作为支持的标志和属性的一组选项。 标志和与各种项类别关联的属性的摘要，请参阅[ **WIA\_IPA\_项\_类别**](https://msdn.microsoft.com/library/windows/hardware/ff551581)。 WIA 项标志的完整列表，请参阅[ **WIA\_IPA\_项\_标志**](https://msdn.microsoft.com/library/windows/hardware/ff551585)。

 

 




