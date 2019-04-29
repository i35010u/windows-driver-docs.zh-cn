---
title: TxtSetup.oem 文件的 Defaults 节
description: 默认值部分列出了支持此文件的每个硬件组件的默认驱动程序。 它向用户呈现的驱动程序列表时，Windows 会突出显示默认选择。
ms.assetid: 5f7fc7c8-543d-442a-911d-320aa19c72f0
keywords:
- Defaults 节 TxtSetup.oem 文件的设备和驱动程序安装
topic_type:
- apiref
api_name:
- Defaults Section of a TxtSetup.oem File
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7c98d6f4028da4a476219e87393a656d8e1e9603
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63369496"
---
# <a name="defaults-section-of-a-txtsetupoem-file"></a>TxtSetup.oem 文件的 Defaults 节


**默认情况下**部分列出了支持此文件的每个硬件组件的默认驱动程序。 它向用户呈现的驱动程序列表时，Windows 会突出显示默认选择。

``` syntax
[Defaults]
component = ID
...
```

<a href="" id="component"></a>*组件*  
指定此文件支持的硬件组件。 *组件*必须是系统定义的以下值之一：**计算机**或**scsi**。

<a href="" id="id"></a>*ID*  
指定一个字符串，标识的默认选项。 此字符串中相应指定 ID 相匹配*HwComponent*部分。

如果*TxtSetup.oem*文件来定义一个受支持组件的默认驱动程序将失败，Windows 将使用中的第一个条目*HwComponent*部分。

下面的示例演示**默认情况下**部分 (并*HwComponent*部分) 对于*TxtSetup.oem*支持一个组件的文件 (**scsi**):

``` syntax
; ...
[Defaults]
SCSI = oemscsi
 
[SCSI]                  ; HwComponent section
oemscsi = "OEM Fast SCSI Controller"
oemscsi2 = "OEM Fast SCSI Controller 2"
 
; ...
```

 

 





