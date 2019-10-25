---
title: MRxCreate 例程
description: TheMRxCreate 例程由 RDBSS 调用，请求网络小型重定向程序创建文件系统对象。
ms.assetid: d1b664cf-37b6-4c65-8634-21695af2db21
keywords:
- MRxCreate 例程可安装文件系统驱动程序
- PMRX_CALLDOWN
topic_type:
- apiref
api_name:
- MRxCreate
api_location:
- mrx.h
api_type:
- UserDefined
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 388b2c2517d02e8906549e7469268a2f79e54984
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72841114"
---
# <a name="mrxcreate-routine"></a>MRxCreate 例程


[RDBSS](https://docs.microsoft.com/windows-hardware/drivers/ifs/the-rdbss-driver-and-library)调用*MRxCreate*例程来请求网络小型重定向程序创建文件系统对象。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxCreate;

NTSTATUS MRxCreate(
  _Inout_ PRX_CONTEXT RxContext
)
{ ... }
```

<a name="parameters"></a>参数
----------

*RxContext* \[in，out\]  
指向 RX\_上下文结构的指针。 此参数包含请求操作的 IRP。

<a name="return-value"></a>返回值
------------

*MRxCreate*返回成功的状态\_成功或使用适当的 NTSTATUS 值，如以下之一：

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
<td align="left"><strong>STATUS_INSUFFICIENT_RESOURCES</strong></td>
<td align="left"><p>资源不足，无法完成此操作。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NETWORK_ACCESS_DENIED</strong></td>
<td align="left"><p>网络访问被拒绝。 如果要求网络小型重定向器在只读共享上打开新文件，则会返回此错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_IMPLEMENTED</strong></td>
<td align="left"><p>未实现请求的功能，如远程启动或远程页面文件。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NOT_SUPPORTED</strong></td>
<td align="left"><p>不支持所请求的功能，如扩展特性。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_OBJECT_NAME_COLLISION</strong></td>
<td align="left"><p>要求网络小型重定向程序创建已存在的文件。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_OBJECT_NAME_NOT_FOUND</strong></td>
<td align="left"><p>找不到对象名称。 如果要求网络小型重定向程序打开不存在的文件，则会返回此错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_OBJECT_PATH_NOT_FOUND</strong></td>
<td align="left"><p>找不到对象路径。 如果请求了 NTFS 流对象，而远程文件系统不支持流，则会返回此错误。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_REPARSE</strong></td>
<td align="left"><p>需要重新分析才能处理符号链接。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_RETRY</strong></td>
<td align="left"><p>应重试该操作。 如果网络小型重定向程序遇到共享冲突或拒绝访问错误，则会返回此错误。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

RDBSS 调用*MRxCreate*来请求网络小型重定向程序通过网络打开文件系统对象。 此调用由 RDBSS 发出，以响应接收[**IRP\_MJ\_创建**](irp-mj-create.md)请求。

在调用*MRxCreate*之前，RDBSS 会修改 RX\_由*RxContext*参数指向的上下文结构：

**pRelevantSrvOpen**设置为 SRV\_开放结构。

**PSrvCall**设置为 SRV\_调用结构。

**NtCreateParameters**设置为请求的 NT\_创建\_参数。

在网络小型重定向程序的上下文中，file 对象指关联的文件控制块（FCB）和文件对象扩展（FOBX）结构。 文件对象与 FOBXs 之间存在一对一的对应关系。 许多文件对象将引用同一 FCB，这表示远程服务器上的单个文件。 客户端可以在同一 FCB 上具有多个不同的打开请求（NtCreateFile 请求），其中每个请求都将创建一个新的文件对象。 RDBSS 和网络小型重定向器可以选择发送比收到的 NtCreateFile 请求更少的*MRxCreate*请求，从而在多个 FOBXs 之间共享 SRV\_开放结构。

如果*MRxCreate*请求用于文件覆盖，并且*MRxCreate*返回状态\_成功，则 RDBSS 将获取分页 i/o 资源并截断文件。 如果缓存管理器正在缓存该文件，RDBSS 将使用刚刚从服务器接收的大小更新缓存管理器的大小。

在返回之前， *MRxCreate*必须设置*RxContext*参数所指向的 RX\_上下文结构的**CurrentIrp&gt;IoStatus。**

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


[**MRxAreFilesAliased**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_chkfcb_calldown)

[**MRxCleanupFobx**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff549841(v=vs.85))

[**MRxCloseSrvOpen**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_calldown)

[**MRxCollapseOpen**](mrxcollapseopen.md)

[**MRxCreate**](mrxcreate.md)

[**MRxDeallocateForFcb**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fcb)

[**MRxDeallocateForFobx**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_deallocate_for_fobx)

[**MRxExtendForCache**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_extendfile_calldown)

[**MRxExtendForNonCache**](mrxextendfornoncache.md)

[**MRxFlush**](mrxflush.md)

[**MRxForceClosed**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_forceclosed_calldown)

[**MRxIsLockRealizable**](https://docs.microsoft.com/windows-hardware/drivers/ddi/mrx/nc-mrx-pmrx_is_lock_realizable)

[**MRxShouldTryToCollapseThisOpen**](mrxshouldtrytocollapsethisopen.md)

[**MRxTruncate**](mrxtruncate.md)

[**MRxZeroExtend**](mrxzeroextend.md)

 

 






