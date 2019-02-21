---
title: IRP_MJ_FILE_SYSTEM_CONTROL
description: 仅文件系统驱动程序处理 IRP_MJ_FILE_SYSTEM_CONTROL 请求。
ms.date: 08/12/2017
ms.assetid: 695ed61b-7082-44be-ae82-ddc3e4a0b8d0
keywords:
- IRP_MJ_FILE_SYSTEM_CONTROL 内核模式驱动程序体系结构
ms.localizationpriority: medium
ms.openlocfilehash: 19cc7c6acd67594e2c6137c50402099a6e18e049
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56555383"
---
# <a name="irpmjfilesystemcontrol"></a>IRP\_MJ\_FILE\_SYSTEM\_CONTROL


只有文件系统驱动程序进程**IRP\_MJ\_文件\_系统\_控制**请求。 有关使用文件系统驱动程序通过此 IRP 主要函数代码的详细信息，请参阅[ **IRP\_MJ\_文件\_系统\_控制**](https://msdn.microsoft.com/library/windows/hardware/ff548670)。 有关文件系统驱动程序的详细信息，请参阅[文件系统驱动程序](https://msdn.microsoft.com/library/windows/hardware/ff540376)。

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
<td>Wdm.h 中 （包括 wdm.h 中、 Ntddk.h 或 Ntifs.h）</td>
</tr>
</tbody>
</table>

 

 




