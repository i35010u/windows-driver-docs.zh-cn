---
title: TxtSetup.oem 文件的 HardwareIds.scsi.ID 节
description: HardwareIds.scsi.ID 节指定硬件特定的大容量存储驱动程序支持的设备的 Id。
ms.assetid: 904744d3-524d-42ea-83a8-1fd7e80d07b8
keywords:
- HardwareIds.scsi.ID 部分中的 TxtSetup.oem 文件的设备和驱动程序安装
topic_type:
- apiref
api_name:
- HardwareIds.scsi.ID Section of a TxtSetup.oem File
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: f20e1b9087716661b9c10571f13c4bebde526ad9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63360603"
---
# <a name="hardwareidsscsiid-section-of-a-txtsetupoem-file"></a>TxtSetup.oem 文件的 HardwareIds.scsi.ID 节


一个**HardwareIds.scsi。**<em>ID</em>节指定硬件特定的大容量存储驱动程序支持的设备的 Id。

``` syntax
[HardwareIds.scsi.ID]
id = "deviceID","service"
...
```

<a href="" id="hardwareids-scsi-id"></a>**HardwareIds.scsi.**<em>ID</em>  
*ID*对应于*ID*中的条目*HwComponent*部分。

<a href="" id="deviceid"></a>*deviceId*  
指定大容量存储设备的设备 ID。

<a href="" id="service"></a>*service*  
指定要为设备安装的服务。 无需其可执行映像文件名指定的服务 *.sys*扩展。

下面的示例是一段摘录**HardwareIds.scsi。**<em>ID</em>磁盘设备的部分：

``` syntax
; ...
[HardwareIds.scsi.oemscsi]
id = "PCI\VEN_9004&DEV_8111","oemscsi"
 
; ... 
```

 

 





