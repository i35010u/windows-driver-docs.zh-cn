---
title: HOST 关闭设备服务
description: 本主题提供适用于移动宽带接口模型（MBIM）的设备的指南，以便在 CID_MBIM_DEVICE_SERVICES 查询时实现和报告所述的设备服务。
ms.assetid: 62BFC796-EDB2-489E-B487-65E2DD7C4256
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 46de4fa87a5b0731f114e4ff80583e457db8b80e
ms.sourcegitcommit: ca5045a739eefd6ed14b9dbd9249b335e090c4e9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2020
ms.locfileid: "85968251"
---
# <a name="host-shutdown-device-service"></a>HOST 关闭设备服务


本主题提供适用于移动宽带接口模型（MBIM）的设备在由 CID \_ MBIM 设备服务查询时实现和报告所述设备服务的指南 \_ \_ 。

本主题中的信息适用于 Windows 8 及更高版本。

## <a name="microsoft-host-shutdown"></a>Microsoft 主机关闭


MBIM 兼容设备在由 CID \_ MBIM 设备服务查询时实现并报告以下设备服务 \_ \_ 。 在[USB NCM 移动宽带接口模型（MBIM） v1.0 规范](https://go.microsoft.com/fwlink/p/?linkid=320791)的第10.1 节中定义了现有的已知服务。 Microsoft 对此进行了扩展，定义了以下服务。

服务名称 = **Microsoft 主机关闭**

UUID = **UUID \_ MS \_ HOSTSHUTDOWN**

UUID 值 = **883b7c26-985f-43fa-9804-27d7fb80959c**

## <a name="defined-cids-for-uuid_ms_hostshutdown-device-service"></a>为 UUID \_ MS \_ HOSTSHUTDOWN 设备服务定义的 cid


| CID                          | 最低操作系统版本       |
|------------------------------|--------------------------|
| CID \_ MBIM \_ MSHOSTSHUTDOWN    | Windows 8                |
| CID \_ MBIM \_ MSHOSTPRESHUTDOWN | Windows 10 版本1511 |

 

## <a name="cid_mbim_mshostshutdown"></a>CID \_ MBIM \_ MSHOSTSHUTDOWN


此命令通知设备主机正在关闭。 MB 设备可能会断电。

**CID**： CID \_ MBIM \_ MSHOSTSHUTDOWN

**命令代码**：1

**设置**：是

**查询**：否

**事件**：否

**设置 InformationBuffer 有效负载**：暂缺

**查询 InformationBuffer 有效负载**：暂缺

**完成 InformationBuffer 有效负载**：暂缺


 

**Set**： \_ 未使用 MBIM 命令消息中的 InformationBuffer \_ 。 未使用 InformationBuffer of MBIM \_ 命令 \_ 。

**查询**：不受支持

**未经许可的事件**：不受支持


 

### <a name="remarks"></a>备注

移动宽带类驱动程序将主机关机通知发送到支持此设备服务的移动宽带设备，并将每个主机状态转换为 S4 和 S5 状态。

此通知旨在提供移动宽带设备，使其能够启动移动网络取消注册消息并启动 SIM 电气反初始化。

以下信息总结了主机向设备发送 Cid/输入的列表，以便进行各种系统转换和设备电源状态转换：

-   将主机状态转换为 S4 和 S5 后，会将 MSHOSTSHUTDOWN CID 发送到设备。
-   \_ \_ 当主机将设备置于 D3 模式下时，会将 MBIM CMD CLOSE 发送到设备。

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"></th>
<th align="left">S0</th>
<th align="left">S1/S2/S3</th>
<th align="left">S4</th>
<th align="left">S5</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>D0</p></td>
<td align="left"><p>MBIM_CMD_OPEN</p></td>
<td align="left"><p>空值</p></td>
<td align="left"><p>空值</p></td>
<td align="left"><p>空值</p></td>
</tr>
<tr class="even">
<td align="left"><p>D1</p></td>
<td align="left"><p>空值</p></td>
<td align="left"><p>空值</p></td>
<td align="left"><p>空值</p></td>
<td align="left"><p>空值</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D2</p></td>
<td align="left"><p>空值</p></td>
<td align="left"><p>空值</p></td>
<td align="left"><p>空值</p></td>
<td align="left"><p>空值</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3</p></td>
<td align="left"><p>空值</p></td>
<td align="left"><p>MBIM_CMD_CLOSE</p></td>
<td align="left"><p>MSHOSTSHUTDOWN</p></td>
<td align="left"><p>MSHOSTSHUTDOWN</p></td>
</tr>
</tbody>
</table>

 

## <a name="cid_mbim_mshostpreshutdown"></a>CID \_ MBIM \_ MSHOSTPRESHUTDOWN


此命令通知 MBIM 调制解调器系统正在预关闭，并且应完成其所有操作，从网络取消注册，并将所需的信息存储到主机上的 flashless 调制解调器事例。 当主机准备进入 S4 和 S5 状态，并等待所有服务正常关闭时，会发送预关闭通知。

**CID**： CID \_ MBIM \_ MSHOSTPRESHUTDOWN

**命令代码**：2

**设置**：是

**查询**：否

**通知**：否

**设置 InformationBuffer 有效负载**：暂缺

**查询 InformationBuffer 有效负载**：暂缺

**完成 InformationBuffer 有效负载**：暂缺


 

参数：

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th align="left"></th>
<th align="left">设置</th>
<th align="left">查询</th>
<th align="left">通知</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left">命令</td>
<td align="left">CID_MBIM_SET_MSHOSTPRESHUTDOWN</td>
<td align="left">空值</td>
<td align="left">空值</td>
</tr>
<tr class="even">
<td align="left">响应</td>
<td align="left">空</td>
<td align="left">空值</td>
<td align="left">空值</td>
</tr>
</tbody>
</table>

 

对于 Set 操作，InformationBuffer 和 InformationBufferLength 为空。

状态代码：

| 状态代码                       | 说明                                                                         |
|-----------------------------------|-------------------------------------------------------------------------------------|
| MBIM \_ 状态 \_ 成功             | 由调制解调器完成的预关闭操作。                                     |
| MBIM \_ 状态 \_ 无 \_ 设备 \_ 支持 | 设备不支持预关闭，并且不需要任何预关闭操作。 |

 

 

 





