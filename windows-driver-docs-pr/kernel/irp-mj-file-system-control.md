---
title: IRP_MJ_FILE_SYSTEM_CONTROL
description: 只有文件系统驱动程序会处理 IRP_MJ_FILE_SYSTEM_CONTROL 请求。
ms.date: 08/12/2017
ms.assetid: 695ed61b-7082-44be-ae82-ddc3e4a0b8d0
keywords:
- IRP_MJ_FILE_SYSTEM_CONTROL 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 1d60cd7a3b98f0fa4f6a0c443bcc3f6e66ee7c57
ms.sourcegitcommit: e6d80e33042e15d7f2b2d9868d25d07b927c86a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/05/2020
ms.locfileid: "91733411"
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

