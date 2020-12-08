---
title: DeviceInfo XML 文档
description: DeviceInfo XML 文档
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f62e35f632e6ea7471455c069e62f8ce04a0730d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782831"
---
# <a name="deviceinfo-xml-document"></a>DeviceInfo XML 文档


"设备和打印机" 用户界面显示有关设备的详细信息，该设备基于设备的元数据包中的 DeviceInfo XML 文档。 此 XML 文档包含指定设备属性的数据，如下所示：

-   设备的功能类别。 此信息由 [**Device.devicecategory**](/previous-versions/windows/hardware/metadata/ff541101(v=vs.85)) xml 元素指定，该元素是 DeviceInfo xml 文档内 [**DeviceCategoryList**](/previous-versions/windows/hardware/metadata/ff541102(v=vs.85)) xml 元素的子元素。

    [**DeviceCategoryList**](/previous-versions/windows/hardware/metadata/ff541102(v=vs.85)) xml 元素中的第一个 [**device.devicecategory**](/previous-versions/windows/hardware/metadata/ff541101(v=vs.85)) xml 元素被视为设备的 *主要功能类别*。 当 "设备和打印机" 用户界面首先显示连接到计算机的设备的 "库" 视图时，或者，如果最终用户已按类别筛选设备，则将基于其主要功能类别显示设备。

    对于多功能设备，附加功能类别由单独的 [**Device.devicecategory**](/previous-versions/windows/hardware/metadata/ff541101(v=vs.85)) xml 子元素指定，该元素遵循 [**DeviceCategoryList**](/previous-versions/windows/hardware/metadata/ff541102(v=vs.85)) XML 元素中的第一个 **device.devicecategory** 元素。 同样，如果最终用户在 "设备和打印机" 用户界面中基于设备类别筛选设备，则将基于其主要和其他功能类别显示设备。

-   设备的型号名称。 此信息由 DeviceInfo XML 文档中的 [**ModelName**](/previous-versions/windows/hardware/metadata/ff549311(v=vs.85)) XML 元素指定。

-   设备的说明。 此信息由 DeviceInfo XML 文档中的 [**DeviceDescription1**](/previous-versions/windows/hardware/metadata/ff541105(v=vs.85)) 和 [**DeviceDescription2**](/previous-versions/windows/hardware/metadata/ff541108(v=vs.85)) XML 元素指定。

-   设备制造商。 此信息由 DeviceInfo XML 文档中的 [**制造商**](/previous-versions/windows/hardware/metadata/ff548710(v=vs.85)) XML 元素指定。

-   表示设备的图标。 此信息由 DeviceInfo XML 文档中的 [**DeviceIconFile**](/previous-versions/windows/hardware/metadata/ff541123(v=vs.85)) XML 元素指定。

    有关设备图标的详细信息，请参阅 [设备图标文件](device-icon-file.md)。

每个设备元数据包必须只包含一个 DeviceInfo XML 文档。 文档的名称必须 DeviceInfo.xml。

DeviceInfo XML 文档中的数据基于 [DEVICEINFO xml 架构](/previous-versions/windows/hardware/metadata/ff541135(v=vs.85))进行格式设置。

 

