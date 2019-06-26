---
title: GDI 信号灯服务
description: GDI 信号灯服务
ms.assetid: b91211a7-19c3-4974-9222-f8eb64c29cc8
keywords:
- GDI WDK Windows 2000 显示，信号量服务
- 图形驱动程序 WDK Windows 2000 显示，信号量的服务
- 绘制 WDK GDI，信号量的服务
- 信号量服务 WDK GDI
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e999becd62ef2e9bdc25231cb262eca2affef6f6
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354726"
---
# <a name="gdi-semaphore-services"></a>GDI 信号灯服务


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
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engacquiresemaphore" data-raw-source="[&lt;strong&gt;EngAcquireSemaphore&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engacquiresemaphore)"><strong>EngAcquireSemaphore</strong></a></p></td>
<td align="left"><p>获取由调用线程具有独占访问权的信号量关联的资源。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatesemaphore" data-raw-source="[&lt;strong&gt;EngCreateSemaphore&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engcreatesemaphore)"><strong>EngCreateSemaphore</strong></a></p></td>
<td align="left"><p>创建信号量对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeletesafesemaphore" data-raw-source="[&lt;strong&gt;EngDeleteSafeSemaphore&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeletesafesemaphore)"><strong>EngDeleteSafeSemaphore</strong></a></p></td>
<td align="left"><p>移除对指定的安全信号量的引用。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeletesemaphore" data-raw-source="[&lt;strong&gt;EngDeleteSemaphore&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engdeletesemaphore)"><strong>EngDeleteSemaphore</strong></a></p></td>
<td align="left"><p>从系统的资源列表中删除信号量对象。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enginitializesafesemaphore" data-raw-source="[&lt;strong&gt;EngInitializeSafeSemaphore&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-enginitializesafesemaphore)"><strong>EngInitializeSafeSemaphore</strong></a></p></td>
<td align="left"><p>初始化指定的安全信号量。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engissemaphoreowned" data-raw-source="[&lt;strong&gt;EngIsSemaphoreOwned&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engissemaphoreowned)"><strong>EngIsSemaphoreOwned</strong></a></p></td>
<td align="left"><p>确定任何线程是否持有指定信号量。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engissemaphoreownedbycurrentthread" data-raw-source="[&lt;strong&gt;EngIsSemaphoreOwnedByCurrentThread&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engissemaphoreownedbycurrentthread)"><strong>EngIsSemaphoreOwnedByCurrentThread</strong></a></p></td>
<td align="left"><p>确定当前正在执行的线程是否持有指定信号量。</p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engreleasesemaphore" data-raw-source="[&lt;strong&gt;EngReleaseSemaphore&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winddi/nf-winddi-engreleasesemaphore)"><strong>EngReleaseSemaphore</strong></a></p></td>
<td align="left"><p>释放指定的信号量。</p></td>
</tr>
</tbody>
</table>

 

 

 





