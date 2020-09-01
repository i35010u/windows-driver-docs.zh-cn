---
title: MRxStop 例程
description: RDBSS 调用 TheMRxStop 例程来停止网络小型重定向程序。
ms.assetid: 7600335e-ab7c-4993-9e27-18e530496b1c
keywords:
- MRxStop 例程可安装文件系统驱动程序
- PMRX_CALLDOWN_CTX
topic_type:
- apiref
api_name:
- MRxStop
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 28f64fc23d3bee382910c6540fab0345d18501d5
ms.sourcegitcommit: 7b9c3ba12b05bbf78275395bbe3a287d2c31bcf4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/28/2020
ms.locfileid: "89066118"
---
# <a name="mrxstop-routine"></a>MRxStop 例程


[RDBSS](./the-rdbss-driver-and-library.md)调用*MRxStop*例程来停止网络小型重定向程序。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN_CTX MRxStop;

NTSTATUS MRxStop(
  _Inout_ PRX_CONTEXT          RxContext,
  _Inout_ PRDBSS_DEVICE_OBJECT RxDeviceObject
)
{ ... }
```

<a name="parameters"></a>parameters
----------

*RxContext* \[in、out\]  
指向 RX \_ 上下文结构的指针。 此参数包含请求网络小型重定向器停止的 IRP。

*RxDeviceObject* \[in、out\]  
指向 \_ \_ 此网络小型重定向程序的 RDBSS 设备对象结构的指针。

<a name="return-value"></a>返回值
------------

*MRxStop* 返回成功的状态 \_ 成功或适当的 NTSTATUS 值，如以下之一：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">返回代码</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><strong>STATUS_REDIRECTOR_HAS_OPEN_HANDLES</strong></td>
<td align="left"><p>网络小型重定向程序具有打开的句柄，可阻止它在此时停止。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_REDIRECTOR_NOT_STARTED</strong></td>
<td align="left"><p>网络小型重定向程序未启动。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

*MRxStop* 从 RDBSS 角度停止并取消网络微型重定向程序。 停止网络小型重定向程序可能需要释放内存分配和其他系统资源。

在调用 *MRxStop*之前，RDBSS 会修改以下值：

RxContext 指向的 RX 上下文结构中的**MajorFunction**成员 \_ 设置*RxContext*为 IRP 的主要功能。

如果是用于停止网络小型重定向器的 RXCONTEXT 请求，则 FsCtl 指向的 RX 上下文结构中的**LowIoContext. ParamsFor. FsCtl. FsControlCode**成员 \_ 设置为 IRP 的 FSTCL 代码。 *RxContext*

RxDeviceObject **StartStopContext.State**指向的 RDBSS \_ 设备对象结构的 StartStopContext 成员 \_ 设置为 "RDBSS *RxDeviceObject* \_ 停止正在 \_ \_ 进行"

RxDeviceObject 指向的 RDBSS 设备对象结构的**StartStopContext. pStopContext**成员 \_ \_ 设置为*RxDeviceObject* *RxContext*参数。

*MRxStop* 由 RDBSS 从 [**RxStopMinirdr**](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstopminirdr) 例程调用。

如果 *MRxStop* 返回状态 \_ SUCCESS，则例程成功。 任何其他返回值都表示在停止网络小型重定向程序时出错。

如果 *MRxStop* 返回 STATUS \_ SUCCESS，则 RDBSS 会将 RDBSS 的状态设置为 RDBSS 可恢复 \_ 。 此状态存储在 RxDeviceObject 指向**StartStopContext.State**的 RDBSS \_ 设备 \_ 对象结构*RxDeviceObject*的 StartStopContext 成员中。

通常，网络小型重定向器会保持一个内部变量，指示网络小型重定向程序是否已启动。 例如，网络小型重定向程序可能会跟踪停止、启动的时间，以及启动操作或停止操作正在进行的时间。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>目标平台</p></td>
<td align="left">桌面型</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Mrx (包含 Mrx) </td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**MRxDevFcbXXXControlFile**](mrxdevfcbxxxcontrolfile.md)

[**MrxStart**](/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown_ctx)

[**RxStopMinirdr**](/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstopminirdr)

 

