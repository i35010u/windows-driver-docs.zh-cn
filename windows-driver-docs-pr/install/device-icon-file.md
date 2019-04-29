---
title: 设备图标文件
description: 设备图标文件
ms.assetid: bd1272d5-f673-4138-887d-94653cf41829
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bf745b5da276f786d08c1ed102f3835d755981f2
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362059"
---
# <a name="device-icon-file"></a>设备图标文件


设备元数据包可以包含一个真实感图像或图标，表示设备和打印机用户界面中的设备。 图像存储在一个图标文件，并必须在指定文件名称[ **DeviceIconFile** ](https://msdn.microsoft.com/library/windows/hardware/ff541123)在包的元素[DeviceInfo XML 文档](deviceinfo-xml-document.md)。

如果设备元数据包不包含设备图标文件和[ **DeviceIconFile** ](https://msdn.microsoft.com/library/windows/hardware/ff541123)元素中，设备和打印机用户界面中显示设备的默认图标。 此图标基于设备的类别类型中指定[ **DeviceCategory** ](https://msdn.microsoft.com/library/windows/hardware/ff541101) DeviceInfo XML 文档的元素。

**请注意**  我们强烈建议设备元数据包包含设备图标文件，用于在设备和打印机用户界面中显示设备的真实感的图像。 详细了解如何创建具有相同的图标显示质量的 Windows 图形元素，请参阅[图标](https://docs.microsoft.com/visualstudio/extensibility/ux-guidelines/images-and-icons-for-visual-studio?view=vs-2017)Microsoft SDK 中。

 

 

 





