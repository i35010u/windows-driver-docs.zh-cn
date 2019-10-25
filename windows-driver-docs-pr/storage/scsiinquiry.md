---
title: ScsiInquiry
description: ScsiInquiry
ms.assetid: a4f6f21c-b096-4a2f-a207-e8618682e780
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 26d3c6f47a20fd6e90d546e96dc9313556d06df9
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842651"
---
# <a name="scsiinquiry"></a>ScsiInquiry


**ScsiInquiry**方法指示一个小型端口驱动程序，该驱动程序管理 iSCSI 发起程序 HBA 以便向目标上的逻辑单元发出 SCSI 查询命令并返回结果。

此 WMI 方法属于未发布的[MSiSCSI\_操作 WMI 类](msiscsi-operations-wmi-class.md)。 有关**ScsiInquiry**方法的参数的说明，请参阅[**ScsiInquiry\_IN**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsiinquiry_in)和[**ScsiInquiry\_OUT**](https://docs.microsoft.com/windows-hardware/drivers/ddi/iscsiop/ns-iscsiop-_scsiinquiry_out)结构的成员说明。

实现 MSiSCSI\_操作 WMI 类的微型端口驱动程序必须支持**ScsiInquiry**。

 

 





