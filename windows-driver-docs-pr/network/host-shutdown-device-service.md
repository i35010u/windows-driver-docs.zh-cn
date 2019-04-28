---
title: HOST 关闭设备服务
description: 本主题提供指南的移动宽带接口模型 (MBIM)-当通过 CID_MBIM_DEVICE_SERVICES 查询符合条件的设备实现并报告所述的设备的服务。
ms.assetid: 62BFC796-EDB2-489E-B487-65E2DD7C4256
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 708a9460279773e71816242146b1f2c44a4564d6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63349648"
---
# <a name="host-shutdown-device-service"></a>HOST 关闭设备服务


本主题提供指南的移动宽带接口模型 (MBIM)-符合条件的设备实现并报告所述的设备服务 CID 进行查询时\_MBIM\_设备\_服务。

本主题中的信息适用于 Windows 8 和更高版本。

## <a name="microsoft-host-shutdown"></a>Microsoft 主机关闭


MBIM 合规的设备实现，并报告以下设备服务 CID 进行查询时\_MBIM\_设备\_服务。 10.1 部分中定义的现有的已知服务[USB NCM 移动宽带接口模型 (MBIM) V1.0 规范](https://go.microsoft.com/fwlink/p/?linkid=320791)。 Microsoft 扩展，以便定义以下服务。

服务名称 = **Microsoft 主机关闭**

UUID = **UUID\_MS\_HOSTSHUTDOWN**

UUID Value = **883b7c26-985f-43fa-9804-27d7fb80959c**

## <a name="defined-cids-for-uuidmshostshutdown-device-service"></a>定义的 UUID Cid\_MS\_HOSTSHUTDOWN 设备服务


| CID                          | 最低操作系统版本       |
|------------------------------|--------------------------|
| CID\_MBIM\_MSHOSTSHUTDOWN    | Windows 8                |
| CID\_MBIM\_MSHOSTPRESHUTDOWN | Windows 10 版本 1511 |

 

## <a name="cidmbimmshostshutdown"></a>CID\_MBIM\_MSHOSTSHUTDOWN


此命令用于指示主机关闭的设备。 MB 设备可能会丢失电源。

|                                      |                           |
|--------------------------------------|---------------------------|
| CID                                  | CID\_MBIM\_MSHOSTSHUTDOWN |
| 命令代码                         | 1                         |
| 设置                                  | 是                       |
| 查询                                | 否                        |
| Event                                | 否                        |
| 设置 InformationBuffer 有效负载        | 不可用                       |
| 查询 InformationBuffer 有效负载      | 不可用                       |
| 完成 InformationBuffer 有效负载 | 不可用                       |

 

|                   |                                                                                                      |
|-------------------|------------------------------------------------------------------------------------------------------|
| 设置               | MBIM 上的 InformationBuffer\_命令\_未使用的消息。 MBIM InformationBuffer\_命令\_未使用的完成。 |
| 查询             | 不支持                                                                                          |
| 未经请求的事件 | 不支持                                                                                          |

 

### <a name="remarks"></a>备注

移动宽带类驱动程序发送到此设备服务，支持每个主机状态转换到状态 S4 和 S5 状态的移动宽带设备主机关闭通知。

此通知是提供的早期迹象，以允许它们启动移动网络的移动宽带设备取消注册消息并启动 SIM 电气取消初始化。

以下信息概述了主机发送给设备的各种系统转换和设备电源状态转换的 Cid/传送的命令的列表：

-   MSHOSTSHUTDOWN CID 发送到主机状态转换到 S4 和 S5 上的设备。
-   MBIM\_CMD\_主机将设备放入 D3 模式时，将关闭发送到设备。

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
<td align="left"><p>不可用</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p>D1</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="odd">
<td align="left"><p>D2</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>不可用</p></td>
</tr>
<tr class="even">
<td align="left"><p>D3</p></td>
<td align="left"><p>不可用</p></td>
<td align="left"><p>MBIM_CMD_CLOSE</p></td>
<td align="left"><p>MSHOSTSHUTDOWN</p></td>
<td align="left"><p>MSHOSTSHUTDOWN</p></td>
</tr>
</tbody>
</table>

 

## <a name="cidmbimmshostpreshutdown"></a>CID\_MBIM\_MSHOSTPRESHUTDOWN


此命令可通知 MBIM 调制解调器系统正在进行预关闭，因此它应完成所有操作，从网络中，取消注册并存储到 flashless 调制解调器情况下的主机的必要信息。 主机正在准备，以便输入状态 S4 和 S5 状态并等待所有服务以适当地关闭时，向下发送预关闭通知。

|                                      |                              |
|--------------------------------------|------------------------------|
| CID                                  | CID\_MBIM\_MSHOSTPRESHUTDOWN |
| 命令代码                         | 2                            |
| 设置                                  | 是                          |
| 查询                                | 否                           |
| 通知                         | 否                           |
| 设置 InformationBuffer 有效负载        | 不可用                          |
| 查询 InformationBuffer 有效负载      | 不可用                          |
| 完成 InformationBuffer 有效负载 | 不可用                          |

 

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
<td align="left">Command</td>
<td align="left">CID_MBIM_SET_MSHOSTPRESHUTDOWN</td>
<td align="left">不可用</td>
<td align="left">不可用</td>
</tr>
<tr class="even">
<td align="left">响应</td>
<td align="left">空</td>
<td align="left">不可用</td>
<td align="left">不可用</td>
</tr>
</tbody>
</table>

 

为设置操作中，InformationBuffer 和 InformationBufferLength 为空。

状态代码：

| 状态代码                       | 描述                                                                         |
|-----------------------------------|-------------------------------------------------------------------------------------|
| MBIM\_状态\_成功             | 通过调制解调器已完成预关机操作。                                     |
| MBIM\_状态\_否\_设备\_支持 | 设备不支持预关闭，并且需要没有预关机操作。 |

 

 

 





