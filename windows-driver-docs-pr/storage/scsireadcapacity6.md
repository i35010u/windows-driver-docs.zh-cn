---
title: ScsiReadCapacity
description: ScsiReadCapacity
ms.assetid: ee4a0d3f-028b-4d25-badf-393198da3191
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 5d6f1c4e72b10134df350e0ef5d71fe65acffb54
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89186662"
---
# <a name="scsireadcapacity"></a>ScsiReadCapacity


**ScsiReadCapacity**方法指示微型端口驱动程序，该驱动程序管理 iSCSI 发起程序 HBA 以登录到目标，并向目标上的逻辑单元发出 SCSI 读取容量命令，然后返回结果。

此 WMI 方法属于未发布的 [MSiSCSI \_ 操作 WMI 类](msiscsi-operations-wmi-class.md)。 有关 **ScsiReadCapacity** 方法的参数的说明，请参阅 [**ScsiReadCapacity \_ IN**](/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsireadcapacity_in) 和 [**ScsiReadCapacity \_ OUT**](/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsireadcapacity_out) 结构的成员说明。

实现 MSiSCSI 操作 WMI 类的微型端口驱动程序 \_ 必须支持 **ScsiReadCapacity**。

 

