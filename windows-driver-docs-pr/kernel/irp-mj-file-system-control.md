---
title: IRP_MJ_FILE_SYSTEM_CONTROL
description: 只有文件系统驱动程序会处理 IRP_MJ_FILE_SYSTEM_CONTROL 请求。
ms.date: 08/12/2017
ms.assetid: 695ed61b-7082-44be-ae82-ddc3e4a0b8d0
keywords:
- IRP_MJ_FILE_SYSTEM_CONTROL 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 4afd6f5d845efa89ef506585274b5c57548d84fd
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89185617"
---
# <a name="irp_mj_file_system_control"></a>IRP \_ MJ \_ 文件 \_ 系统 \_ 控制


仅文件系统驱动程序处理 **IRP \_ MJ \_ 文件 \_ 系统 \_ 控制** 请求。 有关文件系统驱动程序使用此 IRP 主要功能代码的详细信息，请参阅 [**IRP \_ MJ \_ file \_ system \_ CONTROL**](../ifs/irp-mj-file-system-control.md)。 有关文件系统驱动程序的详细信息，请参阅 [文件系统驱动程序](https://docs.microsoft.com/windows-hardware/drivers/ifs/file-system-drivers)。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>标头</p></td>
<td>Wdm.h（包括 Wdm.h、Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

 

