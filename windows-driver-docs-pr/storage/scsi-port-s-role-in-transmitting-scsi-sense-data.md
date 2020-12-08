---
title: SCSI 端口在传输 SCSI 检测数据过程中的角色
description: SCSI 端口在传输 SCSI 检测数据过程中的角色
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 3a6f747a274287a0caa5ce082c3b984e75092f23
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839403"
---
# <a name="scsi-ports-role-in-transmitting-scsi-sense-data"></a>SCSI 端口在传输 SCSI 检测数据过程中的角色


## <span id="ddk_scsi_ports_role_in_transmitting_scsi_sense_data_kg"></span><span id="DDK_SCSI_PORTS_ROLE_IN_TRANSMITTING_SCSI_SENSE_DATA_KG"></span>


每当较高级别的组件（如类驱动程序）请求时，SCSI 端口驱动程序都负责查询设备以获取 SCSI-3 请求感知数据。 若要请求有意义的数据，更高级别的组件必须提供由 SRB 的 **SenseInfoBufferLength** 成员指定的长度的缓冲区，以保留 SRB 的 **SenseInfoBuffer** 成员指向的请求感知数据。 SCSI 端口确定是否在其接收的每个 SRB 中定义这两个字段。 如果已定义，则每当目标控制器返回检查条件以响应 SRB 时，SCSI 端口 furnishes 请求检测数据。

SCSI 端口还负责将请求感知数据转换为适当的 SRB 格式，然后将其存储在 **SenseInfoBuffer** 指向的缓冲区中。

当 SCSI 端口完成 \_ \_ 与 SRB 关联的 IRP MJ SCSI IRP 时，它必须通过将 SRB 的 **SrbStatus** 成员设置为 SRB 状态自动感知 "有效" 来指示它正在返回请求感知信息 \_ \_ \_ 。

 

 




