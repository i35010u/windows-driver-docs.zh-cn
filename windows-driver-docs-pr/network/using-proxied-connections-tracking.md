---
title: 使用代理连接跟踪
description: 使用代理连接跟踪
ms.assetid: 20A737D7-043D-4D05-A15D-85595E48521B
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: cb23ce474690030042163b09c570e203d6630ea6
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63379181"
---
# <a name="using-proxied-connections-tracking"></a>使用代理连接跟踪


Windows 8 和更高版本的 Windows 中支持跟踪通过代理连接。

此 WFP 功能便于跟踪重定向"记录"的与连接的初始重定向到最后一个连接到目标。 WFP 还允许将连接重定向的标注驱动程序。

### <a name="proxied-connections-tracking"></a>通过代理连接跟踪

使用多个代理 （例如，由不同的 Isv 开发） 存在由一方用来与最终目标进行通信的连接可能又被重定向通过第二个参与方;并且，新的连接会再次被重定向原始参与方。 未跟踪的连接，则原始连接可能永远不会达到其最终目标，如陷入无限代理循环。

数据字段标识符，以支持跟踪连接到的新增功能包括：

<a href="" id="fwps-field-xxx-ale-original-app-id"></a>FWPS\_FIELD\_Xxx\_ALE\_ORIGINAL\_APP\_ID  
代理服务器连接的原始应用程序的完整路径。 如果还不是代理应用程序，此路径等同于 xxx\_ALE\_应用\_id。

<a href="" id="fwps-field-xxx-package-id"></a>FWPS\_FIELD\_Xxx\_PACKAGE\_ID  
包标识符是标识关联的 AppContainer 进程的安全标识符 (SID)。 SID 结构的详细信息，请参阅 Microsoft Windows SDK 文档中的 SID 结构的说明。

### <a name="redirecting-connections"></a>将连接重定向

标注驱动程序调用[ **FwpsRedirectHandleCreate0** ](https://msdn.microsoft.com/library/windows/hardware/hh439681)函数来创建可用于 TCP 连接重定向的句柄。

本部分包括以下主题：

使用重定向句柄

查询重定向状态

### <a name="using-a-redirection-handle"></a>使用重定向句柄

ALE 连接之前重定向标注可以连接重定向到本地进程时，必须获得与 FwpsRedirectHandleCreate0 函数的重定向句柄并置于句柄[ **FWPS\_CONNECT\_REQUEST0** ](https://msdn.microsoft.com/library/windows/hardware/ff551231)结构。 标注修改 classifyFn 中的结构，ALE 连接重定向图层。

FWPS\_CONNECT\_REQUEST0 结构包含重定向的以下成员：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">术语</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>localRedirectHandle</strong></p></td>
<td align="left"><p>通过调用创建标注驱动程序的重定向句柄<a href="https://msdn.microsoft.com/library/windows/hardware/hh439681" data-raw-source="[&lt;strong&gt;FwpsRedirectHandleCreate0&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439681)"> <strong>FwpsRedirectHandleCreate0</strong> </a>函数。</p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>localRedirectContext</strong></p></td>
<td align="left"><p>标注驱动程序通过调用分配一个标注驱动程序上下文区域<a href="https://msdn.microsoft.com/library/windows/hardware/ff544520" data-raw-source="[&lt;strong&gt;ExAllocatePoolWithTag&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/ff544520)"> <strong>ExAllocatePoolWithTag</strong> </a>函数。</p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>localRedirectContextSize</strong></p></td>
<td align="left"><p>提供上下文区域的大小，以字节为单位的标注。</p></td>
</tr>
</tbody>
</table>

 

标注驱动程序已完成使用重定向句柄后，它必须调用[ **FwpsRedirectHandleDestroy0** ](https://msdn.microsoft.com/library/windows/hardware/hh439684)函数来销毁句柄。

### <a name="querying-the-redirect-state"></a>查询重定向状态

标注驱动程序调用[ **FwpsQueryConnectionRedirectState0** ](https://msdn.microsoft.com/library/windows/hardware/hh439677)函数以获取连接的重定向状态。 [ **FWPS\_连接\_重定向\_状态**](https://msdn.microsoft.com/library/windows/hardware/hh439704)枚举是对的调用的返回类型**FwpsQueryConnectionRedirectState0**函数。

如果重定向状态为 FWPS\_连接\_不\_重定向，ALE\_CONNECT\_重定向标注可以继续执行代理连接。

如果重定向状态为 FWPS\_连接\_重定向\_BY\_SELF、 ALE\_CONNECT\_重定向标注应返回 FWP\_操作\_允许/FWP\_操作\_继续。

如果重定向状态为 FWPS\_连接\_重定向\_BY\_其他，ALE\_CONNECT\_重定向标注无法转到代理服务器连接如果不信任其他检查器的结果。

如果重定向状态为 FWPS\_连接\_以前\_重定向\_BY\_SELF、 ALE\_CONNECT\_重定向将不能执行重定向标注即使其他检查器的结果不是可接受的。 在这种情况下，它必须允许或阻止连接 (在 ALE\_身份验证\_连接层)。

 

 





