---
title: TxtSetup.oem 文件的 HwComponent 节
description: HwComponent 部分列出了可用于特定组件的驱动程序。 文件支持的每种类型的组件都有一个 HwComponent 部分。
keywords:
- Txtsetup.oem 文件设备和驱动程序安装的 HwComponent 部分
topic_type:
- apiref
api_name:
- HwComponent Section of a TxtSetup.oem File
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: da6bef63fc3b0fadbd2900bfbf061cddc09d4d51
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96826809"
---
# <a name="hwcomponent-section-of-a-txtsetupoem-file"></a>TxtSetup.oem 文件的 HwComponent 节


*HwComponent* 部分列出了可用于特定组件的驱动程序。 文件支持的每种类型的组件都有一个 *HwComponent* 部分。

``` syntax
[HwComponent]
ID = description
...
```

<a href="" id="hwcomponent"></a>*HwComponent*  
节名称必须是以下系统定义的值之一： **计算机** 或 **scsi**。

<a href="" id="id"></a>*识别*  
指定在此部分中唯一的字符串，用于标识选项。

对于本部分中的每个条目，都必须有一个对应的 **文件。**<em>HwComponent</em>**。** 文件中的 <em>ID</em>部分。

对于 **计算机** 组件，字符串的最后三个字符确定哪些内核 Windows 副本。 如果此字符串以 "_up" 结尾，则 Windows 将复制单处理器内核。 如果此字符串以 "_mp" 结尾，则 Windows 将复制多处理器内核。 如果字符串不是以 "_Xp" 结尾，则 Windows 将复制一个或另一个内核，但不保证哪个内核。

<a href="" id="description"></a>*2008*  
指定 Windows 在驱动程序选项菜单中向用户显示的字符串。

下面的示例演示了支持一个组件 (**scsi**) 的 *Txtsetup.oem* 文件的 *HwComponent* 部分，并提供两个选项：

``` syntax
; ...
[SCSI]                  ; HwComponent section
oemscsi = "OEM Fast SCSI Controller"
oemscsi2 = "OEM Fast SCSI Controller 2"
 
; ...
```

 

 





