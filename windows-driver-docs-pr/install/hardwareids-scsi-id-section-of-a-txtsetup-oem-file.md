---
title: TxtSetup.oem 文件的 HardwareIds.scsi.ID 节
description: HardwareIds.scsi.ID 部分指定特定大容量存储驱动程序支持的设备的硬件 Id。
keywords:
- Txtsetup.oem 文件设备和驱动程序安装的 HardwareIds.scsi.ID 部分
topic_type:
- apiref
api_name:
- HardwareIds.scsi.ID Section of a TxtSetup.oem File
api_type:
- NA
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: b51372fe19ef02bac2946be8b795c6b78e519004
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96791769"
---
# <a name="hardwareidsscsiid-section-of-a-txtsetupoem-file"></a>TxtSetup.oem 文件的 HardwareIds.scsi.ID 节


**HardwareIds。**<em>ID</em>部分指定特定大容量存储驱动程序支持的设备的硬件 id。

``` syntax
[HardwareIds.scsi.ID]
id = "deviceID","service"
...
```

<a href="" id="hardwareids-scsi-id"></a>**HardwareIds。**<em>ID</em>  
*Id* 对应于 *HwComponent* 节中的 *id* 条目。

<a href="" id="deviceid"></a>*deviceId*  
指定大容量存储设备的设备 ID。

<a href="" id="service"></a>*服务*  
指定要为设备安装的服务。 服务由其可执行映像的文件名指定，无 *.sys* 扩展名。

下面的示例摘自 **HardwareIds。** 磁盘设备的 <em>ID</em>部分：

``` syntax
; ...
[HardwareIds.scsi.oemscsi]
id = "PCI\VEN_9004&DEV_8111","oemscsi"
 
; ... 
```

 

 





