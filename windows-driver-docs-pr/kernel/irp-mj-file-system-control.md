---
title: IRP_MJ_FILE_SYSTEM_CONTROL
description: 只有文件系统驱动程序会处理 IRP_MJ_FILE_SYSTEM_CONTROL 请求。
ms.date: 08/12/2017
keywords:
- IRP_MJ_FILE_SYSTEM_CONTROL Kernel-Mode 驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 45963dbcc101e48003b3467687827bc0bd23d17a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96839059"
---
# <a name="irp_mj_file_system_control"></a>IRP \_ MJ \_ 文件 \_ 系统 \_ 控制


仅文件系统驱动程序处理 **IRP \_ MJ \_ 文件 \_ 系统 \_ 控制** 请求。 有关文件系统驱动程序使用此 IRP 主要功能代码的详细信息，请参阅 [**IRP \_ MJ \_ file \_ system \_ CONTROL**](../ifs/irp-mj-file-system-control.md)。 有关文件系统驱动程序的详细信息，请参阅 [文件系统驱动程序](../ifs/index.md)。

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

