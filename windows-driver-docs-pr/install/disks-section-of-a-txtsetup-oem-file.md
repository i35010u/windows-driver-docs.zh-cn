---
title: TxtSetup.oem 文件的 Disks 节
description: 磁盘部分标识设备安装工具包中的磁盘。
ms.assetid: 0a1c0bf1-b4b9-45bc-af48-26f19bc72061
keywords:
- TxtSetup.oem 文件的设备和驱动程序安装的磁盘部分
topic_type:
- apiref
api_name:
- Disks Section of a TxtSetup.oem File
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: d7cec3698511bae82b4047404dcf2fe63f1ff236
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63356057"
---
# <a name="disks-section-of-a-txtsetupoem-file"></a>TxtSetup.oem 文件的 Disks 节


**磁盘**部分标识设备安装工具包中的磁盘。 本部分的格式如下：

``` syntax
[Disks]
diskN = "description",tagfile,directory
...
```

<a href="" id="diskn"></a>*diskN*  
指定可以在后续部分中用于标识磁盘的项。

<a href="" id="description"></a>*description*  
指定包含磁盘名称的字符串。 Windows 使用说明来提示用户插入磁盘。

<a href="" id="tagfile"></a>*tagfile*  
指定磁盘上的验证文件的名称。 文件名必须被指定为从根的完整路径，也不能指定一个驱动器。 Windows 将检查此文件以确保用户插入正确的磁盘。

<a href="" id="directory"></a>*directory*  
安装文件的位置在磁盘上指定的目录。 该目录必须指定为从根的完整路径，而且不能指定一个驱动器。

下面的示例演示**磁盘**安装套件，其中包含两个磁盘的部分：

``` syntax
[Disks]
disk1 = "OEM SCSI driver disk 1",\disk1.tag,\
disk2 = "OEM SCSI driver disk 2",\disk2.tag,\
; ...
```

 

 





