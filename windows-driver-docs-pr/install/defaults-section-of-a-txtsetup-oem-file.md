---
title: TxtSetup.oem 文件的 Defaults 节
description: "\"默认\" 部分列出了此文件支持的每个硬件组件) 的默认驱动程序 (。 当 Windows 向用户显示驱动程序列表时，它会突出显示默认选择。"
keywords:
- Txtsetup.oem 文件设备和驱动程序安装的 "默认" 部分
topic_type:
- apiref
api_name:
- Defaults Section of a TxtSetup.oem File
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a53799792049fdd2c300bd30dbc87a6df73de9c3
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96827761"
---
# <a name="defaults-section-of-a-txtsetupoem-file"></a>TxtSetup.oem 文件的 Defaults 节


" **默认** " 部分列出了此文件支持的每个硬件组件) 的默认驱动程序 (。 当 Windows 向用户显示驱动程序列表时，它会突出显示默认选择。

``` syntax
[Defaults]
component = ID
...
```

<a href="" id="component"></a>*组件*  
指定此文件支持的硬件组件。 *组件* 必须是以下系统定义的值之一：**计算机** 或 **scsi**。

<a href="" id="id"></a>*识别*  
指定标识默认选项的字符串。 此字符串与相应 *HwComponent* 部分中指定的 ID 匹配。

如果 *txtsetup.oem* 文件无法为受支持的组件定义默认驱动程序，则 Windows 将使用 *HwComponent* 部分中的第一项。

下面的示例演示了一个 **默认** 节 (和一个 *Txtsetup.oem* 文件的 *HwComponent* 节) ，该文件支持一个组件 (**scsi**) ：

``` syntax
; ...
[Defaults]
SCSI = oemscsi
 
[SCSI]                  ; HwComponent section
oemscsi = "OEM Fast SCSI Controller"
oemscsi2 = "OEM Fast SCSI Controller 2"
 
; ...
```

 

 





