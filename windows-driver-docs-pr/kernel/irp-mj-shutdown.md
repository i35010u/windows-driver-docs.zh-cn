---
title: IRP_MJ_SHUTDOWN
description: 具有内部缓存中对数据的大容量存储设备的驱动程序必须处理此请求 DispatchShutdown 例程中。
ms.date: 08/12/2017
ms.assetid: af0b01b5-5f81-42da-aa4b-433bd422a51f
keywords:
- IRP_MJ_SHUTDOWN 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 5fd060c07e29f5b92188d768dd5facc5d6d85c83
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56561582"
---
# <a name="irpmjshutdown"></a>IRP\_MJ\_SHUTDOWN


数据必须处理此请求中的有内部缓存的大容量存储设备的驱动程序[ *DispatchShutdown* ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)例程。 大容量存储设备的驱动程序和它们的上层的中间驱动程序还如果基础驱动程序维护的数据的内部缓冲区必须处理此请求。

<a name="when-sent"></a>发送时间
---------

收到关闭请求指示的文件系统驱动程序发送请注意，系统正在关闭。

一个或多个文件系统驱动程序可以在用户注销或某些其他原因正在关闭系统时发送这样的较低级驱动程序多个关闭请求。

## <a name="input-parameters"></a>输入参数


无

## <a name="output-parameters"></a>输出参数


无

<a name="operation"></a>操作
---------

该驱动程序必须完成当前缓存在设备中或在完成关闭请求之前保存在驱动程序的内部缓冲区中的任何数据的传输。

驱动程序不会收到**IRP\_MJ\_关闭**请求的设备对象，除非它注册为此，通过[ **IoRegisterShutdownNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549541)或[ **IoRegisterLastChanceShutdownNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549518)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Header</p></td>
<td>Wdm.h 中 （包括 wdm.h 中、 Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

## <a name="see-also"></a>请参阅


[*DispatchShutdown*](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/wdm/nc-wdm-driver_dispatch)

[**IoRegisterLastChanceShutdownNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549518)

[**IoRegisterShutdownNotification**](https://msdn.microsoft.com/library/windows/hardware/ff549541)

 

 




