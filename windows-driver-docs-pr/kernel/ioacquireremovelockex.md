---
title: 保留供系统使用的 Windows 内核例程
description: 保留供系统使用的 Windows 内核例程
ms.assetid: 78b0562a-903a-467d-9bf0-f5499ae47063
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 54c5afb5de5a115a01c6cd46262af346099b38a8
ms.sourcegitcommit: 7500a03d1d57e95377b0b182a06f6c7dcdd4748e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "90102188"
---
# <a name="windows-kernel-routines-reserved-for-system-use"></a>保留供系统使用的 Windows 内核例程


以下例程保留给系统使用：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>例程所返回的值</th>
<th>说明</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>IoAcquireRemoveLockEx</strong></td>
<td><p>请参阅 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)"><strong>IoAcquireRemoveLock</strong></a>。</p></td>
</tr>
<tr class="even">
<td><strong>IoInitializeRemoveLockEx</strong></td>
<td><p>改用 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializeremovelock" data-raw-source="[&lt;strong&gt;IoInitializeRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializeremovelock)"><strong>IoInitializeRemoveLock</strong></a> 。</p></td>
</tr>
<tr class="odd">
<td><strong>IoReleaseRemoveLockAndWaitEx</strong></td>
<td><p>请参阅 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLockAndWait&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait)"><strong>IoReleaseRemoveLockAndWait</strong></a>。</p></td>
</tr>
<tr class="even">
<td><strong>IoReleaseRemoveLockEx</strong></td>
<td><p>请参阅 <a href="/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)"><strong>IoReleaseRemoveLock</strong></a>。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[**IoAcquireRemoveLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioacquireremovelock)  
[**IoInitializeRemoveLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioinitializeremovelock)  
[**IoReleaseRemoveLock**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelock)  
[**IoReleaseRemoveLockAndWait**](/windows-hardware/drivers/ddi/wdm/nf-wdm-ioreleaseremovelockandwait)