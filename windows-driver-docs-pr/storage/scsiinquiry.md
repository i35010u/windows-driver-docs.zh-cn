---
title: ScsiInquiry
description: ScsiInquiry
ms.assetid: a4f6f21c-b096-4a2f-a207-e8618682e780
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 2550938550c2c49f741f6647d65e396d714656d4
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188491"
---
# <a name="scsiinquiry"></a>ScsiInquiry


**ScsiInquiry**方法指示一个小型端口驱动程序，该驱动程序管理 iSCSI 发起程序 HBA 以便向目标上的逻辑单元发出 SCSI 查询命令并返回结果。

此 WMI 方法属于未发布的 [MSiSCSI \_ 操作 WMI 类](msiscsi-operations-wmi-class.md)。 有关 **ScsiInquiry** 方法的参数的说明，请参阅 [**ScsiInquiry \_ IN**](/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsiinquiry_in) 和 [**ScsiInquiry \_ OUT**](/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsiinquiry_out) 结构的成员说明。

实现 MSiSCSI 操作 WMI 类的微型端口驱动程序 \_ 必须支持 **ScsiInquiry**。

 

