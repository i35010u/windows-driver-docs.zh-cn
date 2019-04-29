---
title: DIF_FINISHINSTALL_ACTION
description: DIF_FINISHINSTALL_ACTION
ms.assetid: 76eba79b-7a8a-478e-aaea-8b36eee51846
keywords:
- DIF_FINISHINSTALL_ACTION 设备和驱动程序安装
topic_type:
- apiref
api_name:
- DIF_FINISHINSTALL_ACTION
api_location:
- Setupapi.h
api_type:
- HeaderDef
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 482bdcc0d44a6b63efd41e16aa5b6c80c885a75e
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63362573"
---
# <a name="diffinishinstallaction"></a>DIF_FINISHINSTALL_ACTION


DIF_FINISHINSTALL_ACTION 请求可让安装程序完成安装操作上下文中运行交互式管理员毕竟操作已完成其他设备安装。

### <a name="when-sent"></a>发送时间

在 Windows 8 和更高版本中，完成安装操作也不会自动运行设备安装的一部分。 若要完成设备完成安装操作，用户必须单击"完成安装设备软件"操作中心，以便完成安装。

有关详细信息，请参阅[运行完成安装操作](https://msdn.microsoft.com/library/windows/hardware/ff550700)。

在 Windows 7 中，完成安装过程仅在上下文中运行的具有管理员凭据的用户在以下时间：

-   具有管理员凭据的用户登录时连接该设备的下一次。
-   当重新连接设备。
-   当用户选择扫描硬件更改设备管理器中。

如果用户没有管理权限登录，Windows 将提示用户同意的情况下以及凭据才能在管理员上下文中运行的完成安装操作输入。

### <a name="who-handles"></a>谁处理

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>类共同安装程序</p></td>
<td align="left"><p>可以处理</p></td>
</tr>
<tr class="even">
<td align="left"><p>设备共同安装程序</p></td>
<td align="left"><p>可以处理</p></td>
</tr>
<tr class="odd">
<td align="left"><p>类安装程序</p></td>
<td align="left"><p>可以处理</p></td>
</tr>
</tbody>
</table>

 

### <a name="installer-input"></a>安装程序输入

<a href="" id="deviceinfoset"></a>*DeviceInfoSet*  
句柄[设备信息集](https://msdn.microsoft.com/library/windows/hardware/ff541247)，其中包含要安装的设备。

<a href="" id="deviceinfodata"></a>*DeviceInfoData*  
一个指向[ **SP_DEVINFO_DATA** ](https://msdn.microsoft.com/library/windows/hardware/ff552344)结构，它表示要安装的设备。

<a href="" id="device-installation-parameters-"></a>设备安装参数   
设备安装参数 ( [ **SP_DEVINSTALL_PARAMS** ](https://msdn.microsoft.com/library/windows/hardware/ff552346)结构) 与关联*DeviceInfoData*。

<a href="" id="class-installation-parameters"></a>类的安装参数  
无

### <a name="installer-output"></a>安装程序输出

<a href="" id="device-installation-parameters-"></a>设备安装参数   
如果系统重新启动完成其完成安装操作所必需的安装程序将设置 DI_NEEDREBOOT 标志。

### <a name="installer-return-value"></a>安装程序返回值

安装程序返回了下表中列出的值之一。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">返回值</th>
<th align="left">含义</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>ERROR_DI_DO_DEFAULT</p></td>
<td align="left"><p>安装程序类：安装程序具有未完成安装操作、 已成功完成安装操作，或已确定它不能曾成功完成其完成安装操作。 设备安装应执行默认处理请求。</p>
<p>共同安装程序：共同安装程序不能返回此错误代码。</p></td>
</tr>
<tr class="even">
<td align="left"><p>NO_ERROR</p></td>
<td align="left"><p>安装程序类：类安装程序不应返回此错误代码。 类安装程序将返回此错误代码，设备安装不会执行默认处理请求。</p>
<p>共同安装程序：安装程序具有未完成安装操作、 已成功完成安装操作，或已确定它不能曾成功完成其完成安装操作。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>Win32 错误代码</p></td>
<td align="left"><p>类安装程序或辅助安装程序：安装程序在处理完成安装操作时遇到错误，设备安装应尝试完成下一次设备枚举的管理员上下文中的完成安装操作。</p></td>
</tr>
</tbody>
</table>

 

### <a name="default-dif-code-handler"></a>默认 DIF 代码处理程序

使用 Windows 7 [ **SetupDiFinishInstallAction**](https://msdn.microsoft.com/library/windows/hardware/ff551022)。

没有默认值 DIF 代码处理程序在 Windows 8 和更高版本，并[ **SetupDiFinishInstallAction** ](https://msdn.microsoft.com/library/windows/hardware/ff551022)已删除。

### <a name="comments"></a>备注

因为设备安装不能确定从 ERROR_DI_DO_DEFAULT 返回代码或 NO_ERROR 返回代码完成安装操作是否实际成功，安装程序应通知用户完成安装程序操作的状态。

完成安装操作的详细信息，请参阅[如何设备安装进程完成安装操作](https://msdn.microsoft.com/library/windows/hardware/ff546216)并[实现完成安装操作](https://msdn.microsoft.com/library/windows/hardware/ff546302)。

有关差异代码的常规信息，请参阅[处理 DIF 代码](https://msdn.microsoft.com/library/windows/hardware/ff546094)并[调用默认的 DIF 代码处理程序](https://msdn.microsoft.com/library/windows/hardware/ff537868)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td align="left"><p>Version</p></td>
<td align="left"><p>在 Windows Vista 到 Windows 7 中受支持。</p></td>
</tr>
<tr class="even">
<td align="left"><p>Header</p></td>
<td align="left">Setupapi.h （包括 Setupapi.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[**SetupDiFinishInstallAction**](https://msdn.microsoft.com/library/windows/hardware/ff551022)

 

 






