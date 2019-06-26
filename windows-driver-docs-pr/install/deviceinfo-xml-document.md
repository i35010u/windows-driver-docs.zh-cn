---
title: DeviceInfo XML 文档
description: DeviceInfo XML 文档
ms.assetid: b6b859cf-de30-4df0-bec1-0cd7d8c55ea6
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0932c22db6d3bed51694728fcb27fe76d81d1441
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387113"
---
# <a name="deviceinfo-xml-document"></a>DeviceInfo XML 文档


设备和打印机用户界面显示的设备的基于设备的元数据包中的 DeviceInfo XML 文档相关的详细的信息。 此 XML 文档包含数据的指定设备的属性，如下所示：

-   设备功能类别。 此信息由指定[ **DeviceCategory** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541101(v=vs.85)) XML 元素，它是子元素的[ **DeviceCategoryList** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541102(v=vs.85)) XMLDeviceInfo XML 文档内的元素。

    第一个[ **DeviceCategory** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541101(v=vs.85))中的 XML 元素[ **DeviceCategoryList** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541102(v=vs.85)) XML 元素被视为*主要功能类别*的设备。 当设备和打印机用户界面首次显示的设备的连接到计算机，库视图或最终用户已按类别筛选设备，设备会显示根据其主要功能类别。

    多功能设备的其他功能类别指定通过单独[ **DeviceCategory** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541101(v=vs.85))之后第一个 XML 子元素**DeviceCategory**中的元素[ **DeviceCategoryList** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541102(v=vs.85)) XML 元素。 同样，如果最终用户筛选器基于设备类别的设备和打印机用户界面内的设备，设备会显示根据其主要和附加功能类别。

-   设备的型号名称。 此信息由指定[ **ModelName** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff549311(v=vs.85)) DeviceInfo XML 文档内的 XML 元素。

-   设备的说明。 此信息由指定[ **DeviceDescription1** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541105(v=vs.85))并[ **DeviceDescription2** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541108(v=vs.85)) DeviceInfo XML 内的 XML 元素文档。

-   设备制造商。 此信息由指定[**制造商**](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff548710(v=vs.85)) DeviceInfo XML 文档中的 XML 元素。

-   表示设备的图标。 此信息由指定[ **DeviceIconFile** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541123(v=vs.85)) DeviceInfo XML 文档内的 XML 元素。

    有关设备图标的详细信息，请参阅[设备图标文件](device-icon-file.md)。

每个设备元数据包必须包含一个 DeviceInfo XML 文档。 文档的名称必须是 DeviceInfo.xml。

DeviceInfo XML 文档中的数据的格式根据[DeviceInfo XML 架构](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541135(v=vs.85))。

 

 





