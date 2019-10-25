---
title: ScsiReadCapacity
description: ScsiReadCapacity
ms.assetid: ee4a0d3f-028b-4d25-badf-393198da3191
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a5c8934bc35a74d89a03e860ca8019757bdecb46
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842637"
---
# <a name="scsireadcapacity"></a>ScsiReadCapacity


**ScsiReadCapacity**方法指示微型端口驱动程序，该驱动程序管理 iSCSI 发起程序 HBA 以登录到目标，并向目标上的逻辑单元发出 SCSI 读取容量命令，然后返回结果。

此 WMI 方法属于未发布的[MSiSCSI\_操作 WMI 类](msiscsi-operations-wmi-class.md)。 有关**ScsiReadCapacity**方法的参数的说明，请参阅[**ScsiReadCapacity\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsireadcapacity_in)和[**ScsiReadCapacity\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsireadcapacity_out)结构的成员说明。

实现 MSiSCSI\_操作 WMI 类的微型端口驱动程序必须支持**ScsiReadCapacity**。

 

 





