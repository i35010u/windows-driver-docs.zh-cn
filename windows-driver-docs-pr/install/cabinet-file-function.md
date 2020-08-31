---
title: Cabinet 文件函数
description: Cabinet 文件函数
ms.assetid: 0f72c833-6bcb-4b11-aa7e-dc5cc678836f
keywords:
- Setupapi.log 函数 WDK，cabinet 文件
- .cab 文件
- CAB 文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0007920947177306bf6b4199bb4b6408e5a7d5e
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89096377"
---
# <a name="cabinet-file-function"></a>Cabinet 文件函数





Cabinet (CAB) 文件是一个文件，通常使用。*cab* 扩展，其中包含多个压缩文件作为文件库。 CAB 文件用于组织将复制到用户系统的安装文件。 压缩的文件可以分布在多个 CAB 文件中。

以下函数用于 CAB 文件。 有关详细的函数说明，请参阅 Microsoft Windows SDK 文档。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/setupapi/nf-setupapi-setupiteratecabineta" data-raw-source="[&lt;strong&gt;SetupIterateCabinet&lt;/strong&gt;](/windows/desktop/api/setupapi/nf-setupapi-setupiteratecabineta)"><strong>SetupIterateCabinet</strong></a></p></td>
<td align="left"><p>将通知发送到 CAB 文件中存储的每个文件的回调函数。</p></td>
</tr>
</tbody>
</table>

 

 

