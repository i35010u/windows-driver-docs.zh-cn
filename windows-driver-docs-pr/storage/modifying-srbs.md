---
title: 修改 SRB
description: 修改 SRB
ms.assetid: 9077cfab-c17c-4c8e-9740-0895f227fb4b
keywords:
- SCSI 微型端口驱动程序 WDK 存储 HwScsiStartIo
- HwScsiStartIo
- SRB 修改 WDK 存储
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 853217ec25fc53b1def2901a1193c9b2082cd392
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63355561"
---
# <a name="modifying-srbs"></a>修改 SRB


## <span id="ddk_modifying_srbs_kg"></span><span id="DDK_MODIFYING_SRBS_KG"></span>


如 SCSI 微型端口驱动程序的前面部分中提到[ **DriverEntry** ](https://msdn.microsoft.com/library/windows/hardware/ff552654)例程必须请求端口驱动程序为 SRB 扩展分配内存如果微型端口驱动程序维护每个请求状态信息。

否则，SCSI 微型端口驱动程序可以将值写入到 Srb*仅*出于以下目的和*仅*中以下成员：

-   返回所需的状态中的每个操作的相关**SrbStatus**并**ScsiStatus**成员

-   如果不足发生，以更新**DataTransferLength**成员

-   如果它支持自动请求检测并传输请求检测信息更新**SenseInfoBufferLength**

-   如果 SRB\_标志\_未指定\_中设置方向**SrbFlags**成员和 HBA 是从属 DMA 设备，若要重置 SRB\_标志\_数据\_IN 或 SRB\_标志\_数据\_出时，根据当前的传输请求

-   微型端口驱动程序是否支持八个以上的逻辑单元，以设置**Lun**成员添加到逻辑单元号

如果 HBA 可以处理超过 8 个逻辑单元，指示何时*HwScsiFindAdapter*设置[**端口\_配置\_信息**](https://msdn.microsoft.com/library/windows/hardware/ff563900)，则端口驱动程序不会解释 LUN 信息。 微型端口驱动程序负责映射 8 位 LUN SRB scsi-3 地址，如有必要。

从 8 位 LUN 到 scsi-3 地址的映射是微型端口驱动程序特定。 下表显示了建议的映射，其中*P*是物理的寻址模式， *B*是总线，并且*T*是目标。

8 位 LUN

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

 

SCSI-3 Address

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

 

SCSI 端口驱动程序保留 LUN 0xFF 来指示所有逻辑单元。

 

 




