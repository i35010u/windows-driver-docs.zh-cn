---
title: HwComponent TxtSetup.oem 文件的节
description: HwComponent 部分列出了可用于特定组件的驱动程序。 没有一个 HwComponent 节，用于每种类型的支持文件的组件。
ms.assetid: 84ba057b-6699-4709-bee8-24cb555d4165
keywords:
- HwComponent 部分中的 TxtSetup.oem 文件的设备和驱动程序安装
topic_type:
- apiref
api_name:
- HwComponent Section of a TxtSetup.oem File
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 3f21243aee18b677491771bb518464148b2d7db4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526145"
---
# <a name="hwcomponent-section-of-a-txtsetupoem-file"></a>HwComponent TxtSetup.oem 文件的节


一个*HwComponent*部分列出了可用于特定组件的驱动程序。 没有*HwComponent*部分，了解每种类型的支持文件的组件。

``` syntax
[HwComponent]
ID = description
...
```

<a href="" id="hwcomponent"></a>*HwComponent*  
节的名称必须是系统定义的以下值之一：**计算机**或**scsi**。

<a href="" id="id"></a>*ID*  
指定在本部分中，标识选项中是唯一的字符串。

在本部分中的每个条目，必须具有相应**文件。**<em>HwComponent</em>**。**<em>ID</em>文件中的部分。

有关**计算机**组件，该字符串的最后三个字符确定用于内核 Windows 复制的。 如果此字符串结尾"（_u）"中，Windows 将复制单处理器内核。 如果此字符串中"_mp"结尾，Windows 将复制的多处理器内核。 如果字符串不以"_Xp"结尾，Windows 将复制一个或其他内核，但不保证哪一个。

<a href="" id="description"></a>*description*  
指定 Windows 驱动程序选项的菜单中向用户显示的字符串。

下面的示例演示*HwComponent*部分，了解*TxtSetup.oem*支持一个组件的文件 (**scsi**) 并提供了两个选项：

``` syntax
; ...
[SCSI]                  ; HwComponent section
oemscsi = "OEM Fast SCSI Controller"
oemscsi2 = "OEM Fast SCSI Controller 2"
 
; ...
```

 

 





