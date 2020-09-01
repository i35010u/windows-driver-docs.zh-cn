---
title: WDI_TLV_ASSOCIATION_RESULT_PARAMETERS
description: WDI_TLV_ASSOCIATION_RESULT_PARAMETERS 是包含关联结果的参数的 TLV。
ms.assetid: A6F29084-EF36-43C4-B646-E071E755E110
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ASSOCIATION_RESULT_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 793119e088305af1385ebfcd18bbaa0533c9574e
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89211525"
---
# <a name="wdi_tlv_association_result_parameters"></a>WDI \_ TLV \_ 关联 \_ 结果 \_ 参数


WDI \_ tlv \_ 关联 \_ 结果 \_ 参数是一个 tlv，其中包含关联结果的参数。

## <a name="tlv-type"></a>TLV 类型


0x2D

## <a name="length"></a>Length


Sum (所有包含的元素的大小) 。

## <a name="values"></a>值


| 类型                                                        | 说明                                                                                                                                                                                                                                         |
|-------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32                                                      | 指定 [**WDI 关联 \_ \_ 状态**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_assoc_status)中定义的关联尝试的完成状态。                                                                                                                       |
| UINT32                                                      | 对等方发送的802.11 状态代码，以响应此端口的身份验证或关联请求。                                                                                                                                     |
| UINT8                                                       | 指定端口是否向 AP 发送了802.11 关联或802.11 重新关联请求。 如果使用了重新关联请求，则此值应设置为1。                                                                              |
| [**WDI \_ AUTH \_ 算法**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_auth_algorithm)     | 在关联过程中端口与对等方协商的身份验证算法。                                                                                                                                                             |
| [**WDI \_ 密码 \_ 算法**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm) | 在关联过程中端口与对等方协商的单播密码算法。                                                                                                                                                             |
| [**WDI \_ 密码 \_ 算法**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm) | 多播数据密码算法在关联过程中端口与对等方协商。                                                                                                                                                      |
| [**WDI \_ 密码 \_ 算法**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_cipher_algorithm) | 多播管理密码算法在关联过程中端口与对等方协商。                                                                                                                                                |
| UINT8                                                       | 指定端口是否与支持分发系统 (DS) 服务的对等方关联，该网络中的任何工作站上的 ISO 第2层桥接（包括移动工作站和 Ap）。 如果支持此值，则应将该值设置为1。 |
| UINT8                                                       | 指定在关联操作过程中端口是否已执行端口授权。                                                                                                                                                       |
| UINT8                                                       | 指定是否已为此关联协商 802.11 WMM QoS 协议。 如果已协商该值，此值应设置为1。                                                                                                        |
| [**WDI \_ DS \_ 信息**](/windows-hardware/drivers/ddi/wditypes/ne-wditypes-_wdi_ds_info)                   | 指定端口是否连接到与以前的关联相同的 DS。                                                                                                                                                                 |
| UINT32                                                      | 当 (重新) 关联失败，802.11 的原因代码为30，此值指示对等方请求的关联卷土重来时间的值。                                                                                               |
| WDI \_ 波段 \_ ID (UINT32)                                       | 用于建立关联的带区 ID。                                                                                                                                                                                                |
| UINT32                                                      | IHV 关联状态。 如果关联失败，则它可能包含 IHV 定义的状态代码。 这仅用于调试目的。                                                                                                        |

 

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>最低受支持的客户端</p></td>
<td><p>Windows 10</p></td>
</tr>
<tr class="even">
<td><p>最低受支持的服务器</p></td>
<td><p>Windows Server 2016</p></td>
</tr>
<tr class="odd">
<td><p>标头</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

