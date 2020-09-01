---
title: WIA 项类别
description: WIA 项类别
ms.assetid: b201e365-60d8-4c3b-a9cf-4bbaa318337f
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 785e6aa6a13b096e9fe92dd2b68e4b56913e6a0b
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89189147"
---
# <a name="wia-item-categories"></a>WIA 项类别





本主题适用于 Windows Vista 和更高版本。

WIA 项树中的所有项都必须支持 [**wia \_ IPA \_ item \_ CATEGORY**](./wia-ipa-item-category.md) 属性。 此属性标识项所属的功能类别。 类别确定与项关联的 WIA 项标志集和 WIA 属性集。

WIA 定义以下项类别：

<a href="" id="wia-category-root"></a>WIA \_ 类别 \_ 根  
WIA 扫描器设备的项树中的 *根项* 表示整个设备。 如果设备包含平板、ADF 或胶卷扫描功能，则表示这些输入源的项是根项的子项。 如果设备包含存储，则设备的存储层次结构中最顶层的文件夹项是根项的子项。 应用程序可以通过在根项上实现的 WIA 属性来访问有关设备的信息，包括状态、标识和访问权限。 有关详细信息，请参阅 [实现平板扫描仪项树](implementing-flatbed-scanner-item-trees.md)中的根项属性的讨论，如何 [实现送料扫描器项树](implementing-feeder-scanner-item-trees.md)，如何 [实现胶片扫描器项树](implementing-film-scanner-item-trees.md)。

<a href="" id="wia-category-flatbed"></a>WIA \_ 类别 \_ 平板  
*平台项*表示扫描平板 (也称为 "扫描" 影印) 在 WIA 扫描器设备上。 具有扫描平台的设备的 WIA 项树应包含作为根项的子项的平板项。 此外，如果 WIA 设备支持分段 (例如，通过 [分段筛选器](wia-segmentation-filter.md)) 或多区域扫描，此平板项目应具有子对象（也是平板物品），以表示平板上的单个扫描区域。 子项目（如果存在）应属于与父项相同的 WIA \_ 类别 " \_ 平台" 类别，并且它们应支持 (相同的 wia 属性，并且它们的初始属性值) 与其父级相同，只不过子项目的位置和范围限制为其表示的扫描区域。 如果) 为创建扫描区域提供了一个应用程序，则应用程序可以使用该 WIA 驱动程序的分段筛选器 (，或者微型驱动程序可以自动检测并创建扫描区域本身。 应用程序可以通过平台项 (或项) 上实现的 WIA 属性访问设备的平台扫描功能。 有关详细信息，请参阅 [实现平板扫描仪项树](implementing-flatbed-scanner-item-trees.md)。

<a href="" id="wia-category-feeder"></a>WIA \_ 类别 \_ 馈送器  
" *进纸器" 项* 表示 WIA 扫描器设备上 (ADF) 自动文档送纸器。  (此项类别还可以代表不完全自动并且需要用户手动协助的进纸器，但在这种情况下，WIA 微型驱动程序负责验证下一个文档页在扫描页面之前是否已通过进纸器前进。 ) 带有 ADF 的设备应在其 WIA 项树中包含一个送纸器项。 送纸器项是根项的子项。 应用程序可以通过在馈送器项上实现的 WIA 属性来访问设备的 ADF 扫描功能。 有关详细信息，请参阅 [实现送纸器扫描仪项树](implementing-feeder-scanner-item-trees.md)。

如果 ADF 可以执行双工扫描 (即，扫描文档页的两侧) ，并支持不同的控件设置来扫描文档页的正面和背面，WIA 微型驱动程序应将送纸器前一项和送纸器回送物品作为进纸器项的子项。 应用程序可以通过在送纸器前一项和送送回送物料上实现的 WIA 属性访问 ADF 前部和后扫描功能。 有关这两个项的详细信息，请参阅以下类别说明。

<a href="" id="wia-category-feeder-front"></a>WIA \_ 类别 \_ 馈送器 \_ 前面  
*送纸器前一项*代表用于扫描文档中页面正面的 ADF 设置。 此项目应由一个扫描程序设备的 WIA 微型驱动程序实现，该扫描器设备具有可执行双工扫描并支持用于扫描文档页面正面和背面的不同控制设置的 ADF。 如果设备的 ADF 始终对文档页面的两端使用相同的设置，则该设备不需要此项。 送纸器前一项是送纸器项的子项。 应用程序可以通过在送纸器前一项上实现的 WIA 属性访问 ADF 前台扫描功能。 有关详细信息，请参阅 [实现送纸器扫描仪项树](implementing-feeder-scanner-item-trees.md)。

<a href="" id="wia-category-feeder-back"></a>WIA \_ 类别 \_ 送 \_ 回  
" *送纸器回送" 项* 代表用于扫描文档中页面背面的 ADF 设置。 此项目应由一个扫描程序设备的 WIA 微型驱动程序实现，该扫描器设备具有可执行双工扫描并支持用于扫描文档页面正面和背面的不同控制设置的 ADF。 如果设备的 ADF 始终对文档页面的两端使用相同的设置，则该设备不需要此项。 送纸器回发项是一个送纸器项的子项。 应用程序可以通过在 "送纸器后" 项上实现的 WIA 属性访问 "ADF 回扫描" 功能。 有关详细信息，请参阅 [实现送纸器扫描仪项树](implementing-feeder-scanner-item-trees.md)。

<a href="" id="wia-category-film"></a>WIA \_ 类别 \_ 胶片  
*胶卷项*表示 WIA 扫描仪设备上的电影扫描功能。 作为专用胶片扫描器的设备，或者是配有透明度适配器 (TPA) 的平板扫描仪，应在其 WIA 项树中包含一个或多个电影项。 胶卷项是根项或另一个胶卷项的子项。 作为根项的子项的电影项表示整个扫描图面，此胶卷项可能包含表示扫描图面中对应于各个胶片帧的区域的电影项的子项。 应用程序可以通过在胶片项 (或 items) 上实现的 WIA 属性访问设备的电影扫描功能。 有关详细信息，请参阅 [实现胶片扫描器项树](implementing-film-scanner-item-trees.md)。

<a href="" id="wia-category-folder"></a>WIA \_ 类别 \_ 文件夹  
*文件夹项*表示位于 WIA 扫描器设备内部存储中的一个文件夹。 文件夹项是根项或其他文件夹项的子文件夹。 如果文件夹项有子级，则子项是已完成的文件项和文件夹项的组合。 项树中最顶层的文件夹项是根项的子项。 应用程序可以通过对文件夹项实现的 WIA 属性来访问文件夹内容和有关文件夹的信息。 有关详细信息，请参阅 [WIA 扫描器 Storage](wia-scanner-storage.md)。

<a href="" id="wia-category-finished-file"></a>WIA \_ 类别 \_ 完成 \_ 文件  
*已完成的文件项*表示存储在 WIA 扫描器设备上某个文件夹中的已完成文件。 已完成的文件是其内容不会更改的文件。 此定义排除内容可以动态变化的文件，例如，扫描程序获取并处理图像数据。 已完成的文件项是文件夹项的子文件夹。 应用程序可以通过在完成的文件项上实现的 WIA 属性访问已完成的文件以及有关该文件的信息。 有关详细信息，请参阅 [WIA 扫描器 Storage](wia-scanner-storage.md)。

<a href="" id="wia-category-auto"></a>WIA \_ 类别 \_ 自动  
在 Windows 7 和更高版本中， [自动项](auto-item.md) 表示支持 [自动配置扫描](auto-configured-scanning.md)的 WIA 扫描器设备的自动配置设置。 这种类型的设备可以配置自己的扫描设置，而不需要在台式计算机上运行的 WIA 应用程序配置设置。 例如，如果设备使用户能够从设备 (而不是从应用程序的用户界面启动扫描操作) 并从设备选择操作的输入源，则应用程序可以使用自动项卸载到设备上，配置所选输入源的任务。 自动项是根项的子项。 包含自动项的 WIA 树还必须包含以下一项或多项：平板项目、送纸器项或胶卷项。 应用程序可以通过对根项和自动项实现的 WIA 属性来访问设备的自动配置扫描功能。 有关详细信息，请参阅 [自动项支持的 WIA 属性](wia-properties-supported-by-an-auto-item.md)。

每个 WIA 项类别都有一组必需的 WIA 项标志和 WIA 属性，该类别中的项必须支持该类型的一组标志和属性。 有关与各项类别关联的标志和属性的摘要，请参阅 [**WIA \_ IPA \_ item \_ CATEGORY**](./wia-ipa-item-category.md)。 有关 WIA 项标志的完整列表，请参阅 [**wia \_ IPA \_ item \_ 标志**](./wia-ipa-item-flags.md)。

 

