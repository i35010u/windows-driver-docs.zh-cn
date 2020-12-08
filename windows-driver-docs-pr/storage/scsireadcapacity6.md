---
title: ScsiReadCapacity
description: ScsiReadCapacity
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 7d2b9f3c56e24af5bd4cd125894b7c9b0ac93182
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839395"
---
# <a name="scsireadcapacity"></a>ScsiReadCapacity


**ScsiReadCapacity** 方法指示微型端口驱动程序，该驱动程序管理 iSCSI 发起程序 HBA 以登录到目标，并向目标上的逻辑单元发出 SCSI 读取容量命令，然后返回结果。

此 WMI 方法属于未发布的 [MSiSCSI \_ 操作 WMI 类](msiscsi-operations-wmi-class.md)。 有关 **ScsiReadCapacity** 方法的参数的说明，请参阅 [**ScsiReadCapacity \_ IN**](/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsireadcapacity_in) 和 [**ScsiReadCapacity \_ OUT**](/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsireadcapacity_out) 结构的成员说明。

实现 MSiSCSI 操作 WMI 类的微型端口驱动程序 \_ 必须支持 **ScsiReadCapacity**。

 

