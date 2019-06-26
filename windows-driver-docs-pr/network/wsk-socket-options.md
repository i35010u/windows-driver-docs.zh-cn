---
title: WSK 套接字选项
description: WSK 套接字选项
ms.assetid: 640681a3-ea68-44c5-be2b-a3bc21bfdb7c
ms.date: 07/18/2017
keywords:
- WSK 套接字选项启动 Windows Vista 的网络驱动程序
ms.localizationpriority: medium
ms.openlocfilehash: 5e825b4ca84cf0ac3953f3cc051442a9c1288cce
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67379719"
---
# <a name="wsk-socket-options"></a>WSK 套接字选项


WSK 子系统支持下列套接字选项在 SOL\_套接字级别：

[**SO\_BROADCAST**](https://docs.microsoft.com/windows-hardware/drivers/network/so-broadcast)

[**SO\_CONDITIONAL\_ACCEPT**](https://docs.microsoft.com/windows-hardware/drivers/network/so-conditional-accept)

[**SO\_EXCLUSIVEADDRUSE**](https://docs.microsoft.com/windows-hardware/drivers/network/so-exclusiveaddruse)

[**SO\_KEEPALIVE**](https://docs.microsoft.com/windows-hardware/drivers/network/so-keepalive)

[**SO\_RCVBUF**](https://docs.microsoft.com/windows-hardware/drivers/network/so-rcvbuf)

[**因此\_REUSEADDR**](https://docs.microsoft.com/windows-hardware/drivers/network/so-reuseaddr)

[**SO\_WSK\_EVENT\_CALLBACK**](so-wsk-event-callback.md)

[**SO\_WSK\_SECURITY**](so-wsk-security.md)

基础网络协议可能支持其他套接字选项。

详细了解每个套接字选项，以及有关 SOL 以外的级别上的套接字选项的信息\_套接字，请参阅 Microsoft Windows SDK 文档的"Windows 套接字 2"部分。

<a name="requirements"></a>要求
------------

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Version</p></td>
<td><p>在 Windows Vista 和更高版本的 Windows 操作系统中可用。</p></td>
</tr>
<tr class="even">
<td><p>Header</p></td>
<td>Ws2def.h （包括 Wsk.h）</td>
</tr>
</tbody>
</table>

 

 




