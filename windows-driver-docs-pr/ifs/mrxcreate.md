---
title: MRxCreate 例程
description: TheMRxCreate 例程调用 RDBSS 请求网络微型重定向创建文件系统对象。
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
ms.openlocfilehash: ddbd534db0b801ba91190115e3bf010af23f8962
ms.sourcegitcommit: b3859d56cb393e698c698d3fb13519ff1522c7f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2019
ms.locfileid: "57349464"
---
# <a name="mrxcreate-routine"></a>MRxCreate 例程


*MRxCreate*由调用例程[RDBSS](https://msdn.microsoft.com/library/windows/hardware/ff556810)请求网络微型重定向创建文件系统对象。

<a name="syntax"></a>语法
------

```ManagedCPlusPlus
PMRX_CALLDOWN MRxCreate;

NTSTATUS MRxCreate(
  _Inout_ PRX_CONTEXT RxContext
)
{ ... }
```

<a name="parameters"></a>Parameters
----------

*RxContext* \[in、 out\]  
指向 RX\_上下文结构。 此参数包含 IRP 请求该操作。

<a name="return-value"></a>返回值
------------

*MRxCreate*将返回状态\_成功的成功或相应 NTSTATUS 值，如以下项之一：

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
<td align="left"><p>没有足够的资源来完成该操作。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NETWORK_ACCESS_DENIED</strong></td>
<td align="left"><p>网络访问被拒绝。 如果网络微型重定向已要求打开只读共享上的新文件，可以返回此错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_NOT_IMPLEMENTED</strong></td>
<td align="left"><p>未实现请求，如远程启动或远程的页面文件的功能。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_NOT_SUPPORTED</strong></td>
<td align="left"><p>不支持请求，例如扩展属性的功能。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_OBJECT_NAME_COLLISION</strong></td>
<td align="left"><p>网络微型重定向已要求创建已存在的文件。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_OBJECT_NAME_NOT_FOUND</strong></td>
<td align="left"><p>找不到对象名称。 如果网络微型重定向需要打开的文件不存在，则可以返回此错误。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_OBJECT_PATH_NOT_FOUND</strong></td>
<td align="left"><p>找不到对象路径。 如果请求的 NTFS 流对象和远程文件系统不支持流，可以返回此错误。</p></td>
</tr>
<tr class="even">
<td align="left"><strong>STATUS_REPARSE</strong></td>
<td align="left"><p>重新分析需要处理符号链接。</p></td>
</tr>
<tr class="odd">
<td align="left"><strong>STATUS_RETRY</strong></td>
<td align="left"><p>应重试该操作。 如果网络微型重定向遇到共享冲突或拒绝访问错误，可以返回此错误。</p></td>
</tr>
</tbody>
</table>

 

<a name="remarks"></a>备注
-------

*MRxCreate* RDBSS 请求网络微型-重定向程序在网络上打开的文件系统对象调用。 此调用在接收到响应中颁发 RDBSS [ **IRP\_MJ\_创建**](irp-mj-create.md)请求。

然后再调用*MRxCreate*，RDBSS 修改 RX 中的以下成员\_指向上下文结构*RxContext*参数：

**pRelevantSrvOpen**设置为 SRV\_打开结构。

**Create.pSrvCall**设置为 SRV\_调用结构。

**Create.NtCreateParameters**设置为所请求的 NT\_创建\_参数。

在网络微型重定向的上下文中，文件对象引用的关联的文件控制块 (FCB) 和文件对象的扩展 (FOBX) 结构。 没有文件对象和 FOBXs 之间具有一对一的对应关系。 表示远程服务器上的单个文件的相同 FCB 将引用多个文件对象。 客户端可以对同一 FCB 几个不同的打开请求 （NtCreateFile 请求），其中每项功能将创建一个新的文件对象。 RDBSS 和网络微型-重定向程序可以选择发送更少*MRxCreate*请求数多于 NtCreateFile 接收的请求，有效共享 SRV\_个几个 FOBXs 中打开的结构。

如果*MRxCreate*申请文件覆盖针对的是和*MRxCreate*返回的状态为\_成功，则 RDBSS 将获取分页 I/O 资源，并截断文件。 如果该文件正在缓存的缓存管理器，RDBSS 将更新缓存管理器具有与只是从服务器收到的大小。

在返回之前， *MRxCreate*必须设置**CurrentIrp-&gt;IoStatus.Information** RX 成员\_指向上下文结构*RxContext*参数。

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


[**MRxAreFilesAliased**](https://msdn.microsoft.com/library/windows/hardware/ff549838)

[**MRxCleanupFobx**](https://msdn.microsoft.com/library/windows/hardware/ff549841)

[**MRxCloseSrvOpen**](https://msdn.microsoft.com/library/windows/hardware/ff549845)

[**MRxCollapseOpen**](mrxcollapseopen.md)

[**MRxCreate**](mrxcreate.md)

[**MRxDeallocateForFcb**](https://msdn.microsoft.com/library/windows/hardware/ff549871)

[**MRxDeallocateForFobx**](https://msdn.microsoft.com/library/windows/hardware/ff549872)

[**MRxExtendForCache**](https://msdn.microsoft.com/library/windows/hardware/ff549878)

[**MRxExtendForNonCache**](mrxextendfornoncache.md)

[**MRxFlush**](mrxflush.md)

[**MRxForceClosed**](https://msdn.microsoft.com/library/windows/hardware/ff550677)

[**MRxIsLockRealizable**](https://msdn.microsoft.com/library/windows/hardware/ff550691)

[**MRxShouldTryToCollapseThisOpen**](mrxshouldtrytocollapsethisopen.md)

[**MRxTruncate**](mrxtruncate.md)

[**MRxZeroExtend**](mrxzeroextend.md)

 

 






