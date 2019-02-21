---
title: SCSI 端口的传输 SCSI 检测数据中的角色
description: SCSI 端口的传输 SCSI 检测数据中的角色
ms.assetid: 27acaa0f-5b8f-43a3-9c2b-d23943114335
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5b09b4a68ca4d277ef0036e313ef6fee7870296e
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519032"
---
# <a name="scsi-ports-role-in-transmitting-scsi-sense-data"></a>SCSI 端口的传输 SCSI 检测数据中的角色


## <span id="ddk_scsi_ports_role_in_transmitting_scsi_sense_data_kg"></span><span id="DDK_SCSI_PORTS_ROLE_IN_TRANSMITTING_SCSI_SENSE_DATA_KG"></span>


SCSI 端口驱动程序负责进行更高级别的组件，如类驱动程序，请求它时查询 SCSI 2 请求检测数据的设备。 若要请求检测数据，更高级别的组件必须提供一个指定的长度的缓冲区**SenseInfoBufferLength** SRB 来保存请求检测数据成员指向的**SenseInfoBuffer** SRB 的成员。 SCSI 端口确定是否在收到每个 SRB 中定义的这两个字段。 如果定义了它们，SCSI 端口提供 SCSI 2 请求检测数据，只要目标控制器对 SRB 响应中返回检查条件。

SCSI 端口也是负责存储它所指向的缓冲区中之前将请求检测数据转换为适当的 SRB 格式**SenseInfoBuffer**。

SCSI 端口完成 IRP\_MJ\_SCSI IRP SRB 与相关联，则必须表示它通过设置返回请求检测信息**SrbStatus**成员到 SRB SRB\_状态\_自动感知\_有效。

 

 




