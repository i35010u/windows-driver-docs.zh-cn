---
title: Storport 的角色在传输 SCSI 检测数据
description: Storport 的角色在传输 SCSI 检测数据
ms.assetid: 18f2f4e0-f49b-4026-b18f-26b413f05970
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: bcb042e3344cfeea2937fd2a8b707a29703d31e5
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56543772"
---
# <a name="storports-role-in-transmitting-scsi-sense-data"></a>Storport 的角色在传输 SCSI 检测数据


Storport 驱动程序负责进行更高级别的组件，如类驱动程序，请求它时查询 scsi-3 请求检测数据的设备。 若要请求检测数据，更高级别的组件必须提供一个指定的长度的缓冲区**SenseInfoBufferLength** SRB 来保存请求检测数据成员指向的**SenseInfoBuffer** SRB 的成员。 Storport 确定是否在收到每个 SRB 中定义的这两个字段。 如果定义了它们，Storport 提供 scsi-3 请求检测数据，只要目标控制器对 SRB 响应中返回检查条件。

Storport 程序还负责存储它所指向的缓冲区中之前将请求检测数据转换为适当的 SRB 格式**SenseInfoBuffer**。

Storport 完成 IRP\_MJ\_IRP SCSI SRB 与相关联，则必须表示，它返回请求检测的信息按逻辑 or 操作 SRB\_状态\_自动感知\_有效使用标记**SrbStatus** SRB 的成员。

 

 




