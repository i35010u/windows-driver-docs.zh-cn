---
title: 设备图标文件
description: 设备图标文件
ms.assetid: bd1272d5-f673-4138-887d-94653cf41829
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 4c416bf24d152cc6de61c57e951ccf12117e5e6e
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89095439"
---
# <a name="device-icon-file"></a>设备图标文件


设备元数据包可以在 "设备和打印机" 用户界面中包含一个照片真实的图像（或图标），表示设备。 该图像存储在图标文件中，并且必须在包的[DEVICEINFO XML 文档](deviceinfo-xml-document.md)的[**DeviceIconFile**](/previous-versions/windows/hardware/metadata/ff541123(v=vs.85))元素中指定文件名。

如果设备元数据包不包含设备图标文件和 [**DeviceIconFile**](/previous-versions/windows/hardware/metadata/ff541123(v=vs.85)) 元素，则设备和打印机用户界面将显示该设备的默认图标。 此图标基于在 DeviceInfo XML 文档的 [**device.devicecategory**](/previous-versions/windows/hardware/metadata/ff541101(v=vs.85)) 元素中指定的设备类别类型。

**注意**   强烈建议设备元数据包包含设备图标文件，该文件用于在 "设备和打印机" 用户界面中显示设备的照片真实图像。 有关如何创建具有相同的 Windows 图形元素显示质量的图标的详细信息，请参阅 Microsoft SDK 中的 [图标](/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio?view=vs-2017) 。

 

 

