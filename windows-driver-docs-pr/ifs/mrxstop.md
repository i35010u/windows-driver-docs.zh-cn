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
ms.openlocfilehash: b8b4d2b12d52c667eb3caf818ec4dbe0dbd6176e
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841067"
---
# <a name="mrxstop-routine"></a>MRxStop 例程


[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)调用*MRxStop*例程来停止网络小型重定向程序。

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

<a name="parameters"></a>参数
----------

*RxContext* \[in，out\]  
指向 RX\_上下文结构的指针。 此参数包含请求网络小型重定向器停止的 IRP。

*RxDeviceObject* \[in，out\]  
指向 RDBSS\_设备的指针\_此网络小型重定向程序的对象结构。

<a name="return-value"></a>返回值
------------

*MRxStop*返回成功的状态\_成功或使用适当的 NTSTATUS 值，如以下之一：

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

*MRxStop*从 RDBSS 角度停止并取消网络微型重定向程序。 停止网络小型重定向程序可能需要释放内存分配和其他系统资源。

在调用*MRxStop*之前，RDBSS 会修改以下值：

*RxContext*指向的 RX\_上下文结构中的**MajorFunction**成员设置为 IRP 的主要功能。

如果是用于停止网络小型重定向器的 RXCONTEXT 请求，则*FsCtl*指向的 RX\_上下文结构中的**ParamsFor. FsCtl. FsControlCode**成员设置为 IRP 的 FSTCL 代码。

*RxDeviceObject*所指向的 RDBSS\_设备\_对象结构的**StartStopContext**成员设置为 RDBSS\_停止\_\_进度

*RxDeviceObject*所指向的 RDBSS\_设备\_对象结构的**pStopContext**成员设置为*RxContext*参数。

*MRxStop*由 RDBSS 从[**RxStopMinirdr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstopminirdr)例程调用。

如果*MRxStop*返回 STATUS\_SUCCESS，则例程成功。 任何其他返回值都表示在停止网络小型重定向程序时出错。

如果*MRxStop*返回 STATUS\_SUCCESS，则 RDBSS 会将 RDBSS 的状态设置为 RDBSS\_可。 此状态存储在*RxDeviceObject*指向的 RDBSS\_设备\_对象结构的 StartStopContext 成员中 **。**

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
<td align="left">桌面</td>
</tr>
<tr class="even">
<td align="left"><p>标头</p></td>
<td align="left">Mrx （包括 Mrx）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>另请参阅


[**MRxDevFcbXXXControlFile**](mrxdevfcbxxxcontrolfile.md)

[**MrxStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown_ctx)

[**RxStopMinirdr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nf-mrx-rxstopminirdr)

 

 






