---
title: WDI_TLV_IHV_TASK_DEVICE_CONTEXT
description: WDI_TLV_IHV_TASK_DEVICE_CONTEXT 是包含 IHV 提供的设备上下文的 NDIS_STATUS_WDI_INDICATION_IHV_TASK_REQUEST TLV。
ms.assetid: FBFE8931-DF29-4605-A14D-12CEC0433086
ms.date: 07/18/2017
keywords:
- 从 Windows Vista 开始 WDI_TLV_IHV_TASK_DEVICE_CONTEXT 网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: b9f42ab8d6b3213e04229945447cbd1b28283fd3
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554509"
---
# <a name="wditlvihvtaskdevicecontext"></a>WDI\_TLV\_IHV\_TASK\_DEVICE\_CONTEXT


WDI\_TLV\_IHV\_任务\_设备\_上下文是包含 IHV 提供的设备上下文 TLV [NDIS\_状态\_WDI\_指示\_IHV\_任务\_请求](https://msdn.microsoft.com/library/windows/hardware/dn925637)。

## <a name="tlv-type"></a>TLV 类型


0xE0

## <a name="length"></a>长度


UINT8 元素的数组大小 （以字节为单位）。 该数组必须包含一个或多个元素。

## <a name="values"></a>值


| 在任务栏的搜索框中键入      | 描述                                                                    |
|-----------|--------------------------------------------------------------------------------|
| UINT8\[\] | IHV 提供的设备上下文信息转发到 IHV 任务。 |

 

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

 

 




