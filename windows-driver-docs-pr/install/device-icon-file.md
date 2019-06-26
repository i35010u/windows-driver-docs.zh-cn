---
title: 设备图标文件
description: 设备图标文件
ms.assetid: bd1272d5-f673-4138-887d-94653cf41829
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 992663778df516a07b94c4713cf11b096b37debb
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67387135"
---
# <a name="device-icon-file"></a>设备图标文件


设备元数据包可以包含一个真实感图像或图标，表示设备和打印机用户界面中的设备。 图像存储在一个图标文件，并必须在指定文件名称[ **DeviceIconFile** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541123(v=vs.85))在包的元素[DeviceInfo XML 文档](deviceinfo-xml-document.md)。

如果设备元数据包不包含设备图标文件和[ **DeviceIconFile** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541123(v=vs.85))元素中，设备和打印机用户界面中显示设备的默认图标。 此图标基于设备的类别类型中指定[ **DeviceCategory** ](https://docs.microsoft.com/previous-versions/windows/hardware/metadata/ff541101(v=vs.85)) DeviceInfo XML 文档的元素。

**请注意**  我们强烈建议设备元数据包包含设备图标文件，用于在设备和打印机用户界面中显示设备的真实感的图像。 详细了解如何创建具有相同的图标显示质量的 Windows 图形元素，请参阅[图标](https://docs.microsoft.com/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio?view=vs-2017)Microsoft SDK 中。

 

 

 





