---
title: MRxStop 例程
description: TheMRxStop 例程调用 RDBSS 停止网络微型重定向。
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
ms.openlocfilehash: 8c333347a3a9354e184efcffb0e7b512c8ef3d53
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67384803"
---
# <a name="mrxstop-routine"></a>MRxStop 例程


*MRxStop*由调用例程[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)停止网络微型重定向。

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

<a name="parameters"></a>Parameters
----------

*RxContext* \[in、 out\]  
指向 RX\_上下文结构。 此参数包含请求网络微型-重定向程序停止 IRP。

*RxDeviceObject* \[in、 out\]  
指向 RDBSS\_设备\_此网络微型重定向的对象结构。

<a name="return-value"></a>返回值
------------

*MRxStop*将返回状态\_成功的成功或相应 NTSTATUS 值，如以下项之一：

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
<td align="left"><p>网络微型重定向已打开的句柄会阻止这一次停止的。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_REDIRECTOR_NOT_STARTED</strong></td>
<td align="left"><p>未启动网络微型重定向。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

*MRxStop*停止和取消初始化网络微型-重定向程序从 RDBSS 角度来看。 停止网络微型重定向可能需要释放的内存分配和其他系统资源。

然后再调用*MRxStop*，RDBSS 修改以下值：

**MajorFunction**成员中 RX\_指向上下文结构*RxContext*将设置为 IRP 主要函数。

**LowIoContext.ParamsFor.FsCtl.FsControlCode**成员中 RX\_指向上下文结构*RxContext*设置为 FSCTL 代码 IRP 如果这是用于停止 FSTCL 请求网络微型重定向。

**StartStopContext.State** RDBSS 成员\_设备\_指向对象结构*RxDeviceObject*设置为 RDBSS\_停止\_在\_进度

**StartStopContext.pStopContext** RDBSS 成员\_设备\_指向对象结构*RxDeviceObject*设置为*RxContext*参数。

*MRxStop* RDBSS 从调用[ **RxStopMinirdr** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxstopminirdr)例程。

如果*MRxStop*将返回状态\_成功，则例程是否成功。 任何其他返回值指示错误发生在停止网络微型重定向。

如果*MRxStop*将返回状态\_成功，RDBSS 设置 RDBSS 状态到 RDBSS\_STARTABLE。 此状态存储在**StartStopContext.State** RDBSS 成员\_设备\_指向对象结构*RxDeviceObject*。

网络微型重定向通常会维护一个内部变量，该值指示是否已启动网络微型重定向。 例如，网络微型重定向可能跟踪已停止，启动，以及当启动操作或停止操作正在进行时。

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
<td align="left">桌面设备</td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Mrx.h （包括 Mrx.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**MRxDevFcbXXXControlFile**](mrxdevfcbxxxcontrolfile.md)

[**MrxStart**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nc-mrx-pmrx_calldown_ctx)

[**RxStopMinirdr**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/mrx/nf-mrx-rxstopminirdr)

 

 






