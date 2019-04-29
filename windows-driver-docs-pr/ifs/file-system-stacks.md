---
title: 文件系统堆栈
description: 文件系统堆栈
ms.assetid: 67839ffb-fe38-42c2-8f33-89d01d796d8a
keywords:
- 筛选器驱动程序 WDK 文件系统中，文件系统堆栈
- 文件系统筛选器驱动程序 WDK 中，文件系统堆栈
- 文件系统堆栈 WDK
- WDK 卷文件系统、 设备对象
- VDOs WDK 文件系统
- 控制设备对象 WDK 文件系统
- CDOs WDK 文件系统
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: d4bb14882df90f38400cb7291fd83a03a9e0de59
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63383826"
---
# <a name="file-system-stacks"></a>文件系统堆栈


## <span id="ddk_file_system_stacks_if"></span><span id="DDK_FILE_SYSTEM_STACKS_IF"></span>


文件系统驱动程序创建两个不同类型的设备对象： 控制设备对象 (CDO) 和卷的设备对象 (VDO)。 一个*文件系统堆栈*组成这些设备对象，以及文件系统筛选器驱动程序的附加到其中任何筛选器设备对象之一。 文件系统的设备对象始终窗体堆栈的底部。

### <a name="span-idddkfilesystemcontroldeviceobjectsifspanspan-idddkfilesystemcontroldeviceobjectsifspanfile-system-control-device-objects"></a><span id="ddk_file_system_control_device_objects_if"></span><span id="DDK_FILE_SYSTEM_CONTROL_DEVICE_OBJECTS_IF"></span>文件系统控制设备对象

文件系统控制设备对象表示整个文件系统，而不是单独的卷，并存储在全局文件系统队列中。 文件系统将创建一个或多个命名控件中的设备对象及其**DriverEntry**例程。 例如，FastFat 创建两个 CDOs： 分别用于固定的媒体和可移动介质。 CDFS 创建只有一个 CDO，因为它具有仅可移动介质。

不需要命名为文件系统控制设备对象。 这是因为文件系统筛选器驱动程序，以及许多的内核模式下支持例程，依赖于此卷的设备对象和作为告诉它们相隔的一种方式控制设备对象之间的差异。

### <a name="span-idddkfilesystemvolumedeviceobjectsifspanspan-idddkfilesystemvolumedeviceobjectsifspanfile-system-volume-device-objects"></a><span id="ddk_file_system_volume_device_objects_if"></span><span id="DDK_FILE_SYSTEM_VOLUME_DEVICE_OBJECTS_IF"></span>文件系统卷设备对象

装载文件系统卷的文件系统卷设备对象表示。 装入的卷，通常在对卷装入请求的响应时，文件系统将创建一个卷设备对象。 控制设备对象是卷的设备对象与始终与特定的逻辑或物理存储设备相关联。

**请注意**  与控制设备对象、 不同卷的设备对象必须永远不会命名为，因为命名卷设备对象会在创建安全漏洞。

 

 

 




