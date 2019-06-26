---
title: WDI_TLV_ASSOCIATION_RESULT_PARAMETERS
description: WDI_TLV_ASSOCIATION_RESULT_PARAMETERS 是 TLV，其中包含关联结果的参数。
ms.assetid: A6F29084-EF36-43C4-B646-E071E755E110
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_ASSOCIATION_RESULT_PARAMETERS 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 923874a59e22656858ea1cfa202c84395e494bb0
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67357332"
---
# <a name="wditlvassociationresultparameters"></a>WDI\_TLV\_关联\_结果\_参数


WDI\_TLV\_关联\_结果\_参数是包含参数的关联结果 TLV。

## <a name="tlv-type"></a>TLV 类型


0x2D

## <a name="length"></a>长度


所有包含的元素的大小的总和 （以字节为单位）。

## <a name="values"></a>值


| 在任务栏的搜索框中键入                                                        | 描述                                                                                                                                                                                                                                         |
|-------------------------------------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| UINT32                                                      | 指定关联尝试的完成状态，如中所定义[ **WDI\_ASSOC\_状态**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_assoc_status)。                                                                                                                       |
| UINT32                                                      | 对等方的身份验证或关联请求响应来自此端口发送的 802.11 状态代码。                                                                                                                                     |
| UINT8                                                       | 指定是否端口发送的 802.11 的关联或 802.11 重新关联请求到 AP。 如果使用重新关联请求，此值应设置为 1。                                                                              |
| [**WDI\_身份验证\_算法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_auth_algorithm)     | 该端口关联期间与对等方协商身份验证算法。                                                                                                                                                             |
| [**WDI\_密码\_算法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_cipher_algorithm) | 该端口关联期间与对等方协商单播密码算法。                                                                                                                                                             |
| [**WDI\_密码\_算法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_cipher_algorithm) | 多路广播的数据加密算法，它与对等方协商期间关联端口。                                                                                                                                                      |
| [**WDI\_密码\_算法**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_cipher_algorithm) | 该端口关联期间与对等方协商多播的管理密码算法。                                                                                                                                                |
| UINT8                                                       | 指定是否端口已与对等支持分发系统 (DS) 服务的 ISO 第 2 层桥接 BSS 网络，包括移动工作站和 APs 中的任何工作站上。 如果支持这种情况，此值应设置为 1。 |
| UINT8                                                       | 指定该端口是否已执行关联操作过程中的端口授权。                                                                                                                                                       |
| UINT8                                                       | 指定是否已为该关联协商 802.11 WMM QoS 协议。 此值应设置为 1，如果具有已协商。                                                                                                        |
| [**WDI\_DS\_INFO**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wditypes/ne-wditypes-_wdi_ds_info)                   | 指定该端口连接到同一个 DS 为其以前的关联。                                                                                                                                                                 |
| UINT32                                                      | 时 (re) 关联失败 802.11 原因代码为 30，则此值指示在关联实现重生次请求时，对等方的值。                                                                                               |
| WDI\_BAND\_ID (UINT32)                                      | 带外 ID 在其建立关联。                                                                                                                                                                                                |
| UINT32                                                      | IHV 关联状态。 如果关联失败，这可以包含一个 IHV 定义的状态代码。 这仅用于调试目的。                                                                                                        |

 

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
<td><p>Header</p></td>
<td>Wditypes.hpp</td>
</tr>
</tbody>
</table>

 

 




