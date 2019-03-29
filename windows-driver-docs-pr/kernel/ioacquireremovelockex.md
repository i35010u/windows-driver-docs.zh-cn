---
title: 保留供系统使用的 Windows 内核例程
description: 保留供系统使用的 Windows 内核例程
ms.assetid: 78b0562a-903a-467d-9bf0-f5499ae47063
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: ca65deeb98e548fe40020d4113cae56d56d04664
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56577116"
---
# <a name="windows-kernel-routines-reserved-for-system-use"></a>保留供系统使用的 Windows 内核例程


下面的例程仅供系统使用：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th>例程</th>
<th>描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><strong>IoAcquireRemoveLockEx</strong></td>
<td><p>请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff548204" data-raw-source="[&lt;strong&gt;IoAcquireRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff548204)"> <strong>IoAcquireRemoveLock</strong></a>。</p></td>
</tr>
<tr class="even">
<td><strong>IoInitializeRemoveLockEx</strong></td>
<td><p>使用<a href="https://msdn.microsoft.com/library/windows/hardware/ff549324" data-raw-source="[&lt;strong&gt;IoInitializeRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549324)"> <strong>IoInitializeRemoveLock</strong> </a>相反。</p></td>
</tr>
<tr class="odd">
<td><strong>IoReleaseRemoveLockAndWaitEx</strong></td>
<td><p>请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff549567" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLockAndWait&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549567)"> <strong>IoReleaseRemoveLockAndWait</strong></a>。</p></td>
</tr>
<tr class="even">
<td><strong>IoReleaseRemoveLockEx</strong></td>
<td><p>请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff549560" data-raw-source="[&lt;strong&gt;IoReleaseRemoveLock&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff549560)"> <strong>IoReleaseRemoveLock</strong></a>。</p></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[**IoAcquireRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff548204)  
[**IoInitializeRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff549324)  
[**IoReleaseRemoveLock**](https://msdn.microsoft.com/library/windows/hardware/ff549560)  
[**IoReleaseRemoveLockAndWait**](https://msdn.microsoft.com/library/windows/hardware/ff549567)  



