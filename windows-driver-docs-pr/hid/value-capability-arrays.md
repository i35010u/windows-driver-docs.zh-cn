---
title: 值功能数组
description: 值功能数组
ms.assetid: d447dda6-a1e5-4e57-b06f-f79f8662c236
keywords:
- 值功能数组 WDK HID
- WDK HID 的数组
- 功能 WDK HID 集合
- 使用值数组 WDK HID
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d9ed2b21572e0beae894dd22b084be1c6593098d
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385792"
---
# <a name="value-capability-arrays"></a>值功能数组





一个*值功能数组*包含有关支持的值使用情况的信息[顶级集合](top-level-collections.md)HID 报表为特定类型。 有关集合的值功能数组的信息包含在其[ **HIDP\_CAP** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/ns-hidpi-_hidp_caps)结构。

用户模式应用程序或内核模式驱动程序将使用以下值之一[HIDClass 支持例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/index)获取按钮功能的信息：

-   [**HidP\_GetValueCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_getvaluecaps)返回描述调用方指定的报告类型中包含的所有值的值功能数组。

-   [**HidP\_GetSpecificValueCaps** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_getspecificvaluecaps)筛选它将返回由调用方指定的使用情况页面、 使用情况、 链接集合和报告类型的值功能信息。

值功能包含一个数组[ **HIDP\_值\_CAPS** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/ns-hidpi-_hidp_value_caps)结构，其中每个以下信息介绍[的HID用途](hid-usages.md)或[使用范围](hid-usages.md#usage-range):

-   [使用情况页面](hid-usages.md#usage-page)的使用情况或使用范围

-   包含的值的报表的报表 ID

-   一个[用法 ID](hid-usages.md#usage-id)或使用范围

-   指示是否使用[别名使用情况](hid-usages.md#aliased-usages)

-   有关的信息[集合链接](link-collections.md)，其中包含的使用情况或使用范围

-   大小，以位为单位的值，并报告计数 （即结构所描述的单个值的数目）

-   每个值的属性包括： 是否有 null 值、 其单位和指数和其逻辑和物理范围

-   有关字符串描述符和使用情况或使用区域相关联的指示符的信息

-   有关的信息[数据索引](data-indices.md)HID 分析器指定一种使用情况或使用范围

一般情况下，值功能数组所描述的所有用法都具备以下条件：

-   每个功能结构表示使用情况，使用范围，或[用法值数组](#usage-value-array)变量主要项与该键相关联。 数组的主要项目不支持的值。

-   可以使用别名用法。 使用范围不能有别名。 使用别名值链接在一起值功能数组中使用别名按钮作为链接按钮功能数组在一起的方式相同。 请参阅[按钮变量主要项中的用法](button-capability-arrays.md#button-usages-in-a-variable-main-item)。

-   HID 分析器使用的最小所需的用法将用量分配给每个值。 分析器将分配的报告描述符中指定的顺序的用法。 不是必需的报表描述符中使用实例将被丢弃。 值功能数组不包含任何有关放弃用法的信息。

-   HID 分析器将分配一个唯一[数据索引](data-indices.md)功能数组中所述的每个使用情况。

有关如何将数据索引分配到值的说明，请参阅[数据索引](data-indices.md)。

### <a href="" id="usage-value-array"></a> 使用值数组

一个*用法值数组*是一组连续的值指定在主要项中，所有这些分配相同的使用情况。 如果只有一种用法指定为其报告计数大于 1 的主要项，将发生这种情况。

下图显示了使用情况值数组，其中包含五个数据项，每个六位长的示例。

![说明使用值数组，其中包含五个数据项，每个 6 位长的关系图](images/repcount.png)

此类的用法值数组的值功能结构必须在上一示例中，其**IsRange**成员设置为**FALSE**，将其**NotRange.Usage**成员设置为 17，其**ReportCount**成员设置为 5，并将其**BitSize**成员设置为 6。

如果使用情况报告计数为 1，则使用**HidP\_GetUsageValue**提取使用情况值。 如果使用的报表计数大于 1， **HidP\_GetUsageValue**仅使用值数组中返回第一个数据项。 若要提取使用情况值数组中的所有数据项，请使用[ **HidP\_GetUsageValueArray**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/hidpi/nf-hidpi-hidp_getusagevaluearray)。

 

 




