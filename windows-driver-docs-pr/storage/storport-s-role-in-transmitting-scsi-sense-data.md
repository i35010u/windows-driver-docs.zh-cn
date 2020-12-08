---
title: Storport 在传输 SCSI 检测数据过程中的角色
description: Storport 在传输 SCSI 检测数据过程中的角色
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 44aa574621065d3221495cee3034903ad5dfa7b8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96820501"
---
# <a name="storports-role-in-transmitting-scsi-sense-data"></a>Storport 在传输 SCSI 检测数据过程中的角色


如果某个高级组件（如类驱动程序）请求，则该 Storport 驱动程序负责在设备中查询 SCSI-3 请求感知数据。 若要请求有意义的数据，更高级别的组件必须提供由 SRB 的 **SenseInfoBufferLength** 成员指定的长度的缓冲区，以保留 SRB 的 **SenseInfoBuffer** 成员指向的请求感知数据。 Storport 确定是否在其接收的每个 SRB 中定义这两个字段。 如果定义了这些选项，则每当目标控制器返回检查条件以响应 SRB 时，furnishes 会请求检测数据。

Storport 还负责将请求感知数据转换为适当的 SRB 格式，然后将其存储在 **SenseInfoBuffer** 指向的缓冲区中。

当 Storport 完成 \_ \_ 与 SRB 关联的 IRP MJ SCSI IRP 时，它必须指示它是通过 OR 的 SRB \_ 状态自动 \_ 感知中的 \_ 有效标志，并在 SRB 的 **SrbStatus** 成员返回请求感知信息。

 

 




