---
title: TxtSetup.oem 文件的 Disks 节
description: 磁盘部分标识设备安装工具包中的磁盘。
keywords:
- Txtsetup.oem 文件设备和驱动程序安装的磁盘部分
topic_type:
- apiref
api_name:
- Disks Section of a TxtSetup.oem File
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 112c5ebe672643f28ce13f5796fdba5f80a9ba3c
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96782745"
---
# <a name="disks-section-of-a-txtsetupoem-file"></a>TxtSetup.oem 文件的 Disks 节


**磁盘** 部分标识设备安装工具包中的磁盘。 此部分具有以下格式：

``` syntax
[Disks]
diskN = "description",tagfile,directory
...
```

<a href="" id="diskn"></a>*diskN*  
指定可在后续部分中用于标识磁盘的密钥。

<a href="" id="description"></a>*2008*  
指定包含磁盘名称的字符串。 Windows 使用描述来提示用户插入磁盘。

<a href="" id="tagfile"></a>*tagfile*  
指定磁盘上验证文件的名称。 必须将 filename 指定为根的完整路径，并且不得指定驱动器。 Windows 将检查此文件以确保用户插入了正确的磁盘。

<a href="" id="directory"></a>*文件夹*  
指定安装文件所在磁盘上的目录。 目录必须指定为根目录的完整路径，并且不得指定驱动器。

以下示例显示了包含两个磁盘的安装工具包的 **磁盘** 部分：

``` syntax
[Disks]
disk1 = "OEM SCSI driver disk 1",\disk1.tag,\
disk2 = "OEM SCSI driver disk 2",\disk2.tag,\
; ...
```

 

 





