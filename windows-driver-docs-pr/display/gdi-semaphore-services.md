---
title: GDI 信号量服务
description: GDI 信号量服务
ms.assetid: b91211a7-19c3-4974-9222-f8eb64c29cc8
keywords:
- GDI WDK Windows 2000 显示，信号量服务
- 图形驱动程序 WDK Windows 2000 显示，信号量的服务
- 绘制 WDK GDI，信号量的服务
- 信号量服务 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9a399913fed70ed620a0fc18d6af0661b68621b4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56519259"
---
# <a name="gdi-semaphore-services"></a>GDI 信号量服务


## <span id="ddk_gdi_semaphore_services_gg"></span><span id="DDK_GDI_SEMAPHORE_SERVICES_GG"></span>


GDI 提供一系列与信号量和安全的信号量相关的服务。 驱动程序可以使用这些服务创建或删除一个信号量，并获取或释放信号量。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">函数</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564174" data-raw-source="[&lt;strong&gt;EngAcquireSemaphore&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564174)"><strong>EngAcquireSemaphore</strong></a></p></td>
<td align="left"><p>获取由调用线程具有独占访问权的信号量关联的资源。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564760" data-raw-source="[&lt;strong&gt;EngCreateSemaphore&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564760)"><strong>EngCreateSemaphore</strong></a></p></td>
<td align="left"><p>创建信号量对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564814" data-raw-source="[&lt;strong&gt;EngDeleteSafeSemaphore&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564814)"><strong>EngDeleteSafeSemaphore</strong></a></p></td>
<td align="left"><p>移除对指定的安全信号量的引用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564819" data-raw-source="[&lt;strong&gt;EngDeleteSemaphore&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564819)"><strong>EngDeleteSemaphore</strong></a></p></td>
<td align="left"><p>从系统中删除信号量对象&#39;s 资源列表。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564959" data-raw-source="[&lt;strong&gt;EngInitializeSafeSemaphore&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564959)"><strong>EngInitializeSafeSemaphore</strong></a></p></td>
<td align="left"><p>初始化指定的安全信号量。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564960" data-raw-source="[&lt;strong&gt;EngIsSemaphoreOwned&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564960)"><strong>EngIsSemaphoreOwned</strong></a></p></td>
<td align="left"><p>确定任何线程是否持有指定信号量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff564961" data-raw-source="[&lt;strong&gt;EngIsSemaphoreOwnedByCurrentThread&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff564961)"><strong>EngIsSemaphoreOwnedByCurrentThread</strong></a></p></td>
<td align="left"><p>确定当前正在执行的线程是否持有指定信号量。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff565004" data-raw-source="[&lt;strong&gt;EngReleaseSemaphore&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff565004)"><strong>EngReleaseSemaphore</strong></a></p></td>
<td align="left"><p>释放指定的信号量。</p></td>
</tr>
</tbody>
</table>

 

 

 





