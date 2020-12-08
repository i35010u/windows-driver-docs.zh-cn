---
title: 修改 SRB
description: 修改 SRB
keywords:
- SCSI 微型端口驱动程序 WDK 存储，HwScsiStartIo
- HwScsiStartIo
- SRB 修改 WDK 存储
ms.date: 10/08/2019
ms.localizationpriority: medium
ms.openlocfilehash: 88d736826409cca32cb58b7f1f331e3d83c455b8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96835047"
---
# <a name="modifying-srbs"></a>修改 SRB

如前面部分所述，如果微型端口驱动程序维护每个请求的状态信息，则 SCSI 微型端口驱动程序的 [**DriverEntry**](driverentry-of-scsi-miniport-driver.md) 例程必须请求端口驱动程序为 SRB 扩展插件分配内存。

否则，SCSI 微型端口驱动程序只能出于以下目的将值写入 *到 SRBs* 中 *only* ：

- 返回 **SrbStatus** 和 **ScsiStatus** 成员中有关每个操作的所需状态

- 如果发生不足，则更新 **DataTransferLength** 成员

- 如果它支持自动请求识别并传输请求感知信息，则更新 **SenseInfoBufferLength**

- 如果 SRB_FLAGS_UNSPECIFIED_DIRECTION 在 **SrbFlags** 成员中设置，并且 HBA 是从属 DMA 设备，则根据当前传输请求重置 SRB_FLAGS_DATA_IN 或 SRB_FLAGS_DATA_OUT

- 如果微型端口驱动程序支持8个以上的逻辑单元，则将 **Lun** 成员设置为逻辑单元号

如果 HBA 可以处理超过八个逻辑单元，如 *HwScsiFindAdapter* 设置 [PORT_CONFIGURATION_INFORMATION](/windows-hardware/drivers/ddi/srb/ns-srb-_port_configuration_information)时所指示的那样，端口驱动程序不会解释 LUN 信息。 如果需要，微型端口驱动程序负责将8位 LUN 从 SRB 映射到 SCSI-3 地址。

从8位 LUN 到 SCSI-3 地址的映射是特定于微型端口驱动程序。 下表显示了建议的映射，其中 *P* 为物理寻址模式， *B* 为总线， *T* 为目标。

8位 LUN

<table>
<colgroup>
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>位/字节</p></td>
<td align="left"><p>7</p></td>
<td align="left"><p>6</p></td>
<td align="left"><p>5</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>3</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0</p></td>
<td align="left"><p>P</p></td>
<td align="left"><p>P</p></td>
<td align="left"><p>B</p></td>
<td align="left"><p>B</p></td>
<td align="left"><p>T</p></td>
<td align="left"><p>T</p></td>
<td align="left"><p>T</p></td>
<td align="left"><p>T</p></td>
</tr>
</tbody>
</table>

SCSI-3 地址

<table>
<colgroup>
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
<col width="11%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>位/字节</p></td>
<td align="left"><p>7</p></td>
<td align="left"><p>6</p></td>
<td align="left"><p>5</p></td>
<td align="left"><p>4</p></td>
<td align="left"><p>3</p></td>
<td align="left"><p>2</p></td>
<td align="left"><p>1</p></td>
<td align="left"><p>0</p></td>
</tr>
<tr class="even">
<td align="left"><p>0</p></td>
<td align="left"><p>P</p></td>
<td align="left"><p>P</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>B</p></td>
<td align="left"><p>B</p></td>
</tr>
<tr class="odd">
<td align="left"><p>1</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>0</p></td>
<td align="left"><p>T</p></td>
<td align="left"><p>T</p></td>
<td align="left"><p>T</p></td>
<td align="left"><p>T</p></td>
</tr>
</tbody>
</table>

SCSI 端口驱动程序保留 LUN 0xFF 以指示所有逻辑单元。
