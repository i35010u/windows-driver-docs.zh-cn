---
title: DeviceInfo XML 文档
description: DeviceInfo XML 文档
ms.assetid: b6b859cf-de30-4df0-bec1-0cd7d8c55ea6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4b2441f9d33f9f594a618d3b4ad9858459255240
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56568083"
---
# <a name="deviceinfo-xml-document"></a>DeviceInfo XML 文档


设备和打印机用户界面显示的设备的基于设备的元数据包中的 DeviceInfo XML 文档相关的详细的信息。 此 XML 文档包含数据的指定设备的属性，如下所示：

-   设备功能类别。 此信息由指定[ **DeviceCategory** ](https://msdn.microsoft.com/library/windows/hardware/ff541101) XML 元素，它是子元素的[ **DeviceCategoryList** ](https://msdn.microsoft.com/library/windows/hardware/ff541102) XMLDeviceInfo XML 文档内的元素。

    第一个[ **DeviceCategory** ](https://msdn.microsoft.com/library/windows/hardware/ff541101)中的 XML 元素[ **DeviceCategoryList** ](https://msdn.microsoft.com/library/windows/hardware/ff541102) XML 元素被视为*主要功能类别*的设备。 当设备和打印机用户界面首次显示的设备的连接到计算机，库视图或最终用户已按类别筛选设备，设备会显示根据其主要功能类别。

    多功能设备的其他功能类别指定通过单独[ **DeviceCategory** ](https://msdn.microsoft.com/library/windows/hardware/ff541101)之后第一个 XML 子元素**DeviceCategory**中的元素[ **DeviceCategoryList** ](https://msdn.microsoft.com/library/windows/hardware/ff541102) XML 元素。 同样，如果最终用户筛选器基于设备类别的设备和打印机用户界面内的设备，设备会显示根据其主要和附加功能类别。

-   设备的型号名称。 此信息由指定[ **ModelName** ](https://msdn.microsoft.com/library/windows/hardware/ff549311) DeviceInfo XML 文档内的 XML 元素。

-   设备的说明。 此信息由指定[ **DeviceDescription1** ](https://msdn.microsoft.com/library/windows/hardware/ff541105)并[ **DeviceDescription2** ](https://msdn.microsoft.com/library/windows/hardware/ff541108) DeviceInfo XML 内的 XML 元素文档。

-   设备制造商。 此信息由指定[**制造商**](https://msdn.microsoft.com/library/windows/hardware/ff548710) DeviceInfo XML 文档中的 XML 元素。

-   表示设备的图标。 此信息由指定[ **DeviceIconFile** ](https://msdn.microsoft.com/library/windows/hardware/ff541123) DeviceInfo XML 文档内的 XML 元素。

    有关设备图标的详细信息，请参阅[设备图标文件](device-icon-file.md)。

每个设备元数据包必须包含一个 DeviceInfo XML 文档。 文档的名称必须是 DeviceInfo.xml。

DeviceInfo XML 文档中的数据的格式根据[DeviceInfo XML 架构](https://msdn.microsoft.com/library/windows/hardware/ff541135)。

 

 





