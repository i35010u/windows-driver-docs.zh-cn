---
title: 客户端对象和引擎
description: 客户端对象和引擎
ms.assetid: 959912c0-bce9-4d5b-9119-1ac07a8ea1ad
keywords:
- EngExtCpp 扩展，客户端对象
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 6f403828220749a4e67121400096d2a18df72ce9
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63375095"
---
# <a name="client-objects-and-the-engine"></a>客户端对象和引擎


## <span id="ddk_using_clients_and_the_engine_dbx"></span><span id="DDK_USING_CLIENTS_AND_THE_ENGINE_DBX"></span>


与 EngExtCpp 扩展交互[调试器引擎](introduction.md#debugger-engine)通过客户端对象。 对客户端对象的接口指针可供通过成员的扩展[ **ExtExtension** ](https://msdn.microsoft.com/library/windows/hardware/ff543981)基类。 以下成员提供对引擎 API 接口的第一个版本的访问。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">引擎 API 接口</th>
<th align="left">ExtExtension 成员</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549798" data-raw-source="[IDebugAdvanced](https://msdn.microsoft.com/library/windows/hardware/ff549798)">IDebugAdvanced</a></p></td>
<td align="left"><p><strong>m_Advanced</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff549827" data-raw-source="[IDebugClient](https://msdn.microsoft.com/library/windows/hardware/ff549827)">IDebugClient</a></p></td>
<td align="left"><p><strong>m_Client</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550508" data-raw-source="[IDebugControl](https://msdn.microsoft.com/library/windows/hardware/ff550508)">IDebugControl</a></p></td>
<td align="left"><p><strong>m_Control</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550528" data-raw-source="[IDebugDataSpaces](https://msdn.microsoft.com/library/windows/hardware/ff550528)">IDebugDataSpaces</a></p></td>
<td align="left"><p><strong>m_Data</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550825" data-raw-source="[IDebugRegisters](https://msdn.microsoft.com/library/windows/hardware/ff550825)">IDebugRegisters</a></p></td>
<td align="left"><p><strong>m_Registers</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550856" data-raw-source="[IDebugSymbols](https://msdn.microsoft.com/library/windows/hardware/ff550856)">IDebugSymbols</a></p></td>
<td align="left"><p><strong>m_Symbols</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://msdn.microsoft.com/library/windows/hardware/ff550875" data-raw-source="[IDebugSystemObjects](https://msdn.microsoft.com/library/windows/hardware/ff550875)">IDebugSystemObjects</a></p></td>
<td align="left"><p><strong>m_System</strong></p></td>
</tr>
</tbody>
</table>

 

以下成员提供更高版本的引擎 API 接口的访问权限。 这些接口可能的调试器引擎的所有版本中可用。 如果它们不可用，任何尝试使用它们将导致引发异常。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">引擎 API 接口</th>
<th align="left">ExtExtension 成员</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p><strong>IDebugAdvanced2</strong></p></td>
<td align="left"><p><strong>m_Advanced2</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IDebugAdvanced3</strong></p></td>
<td align="left"><p><strong>m_Advanced3</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IDebugClient2</strong></p></td>
<td align="left"><p><strong>m_Client2</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IDebugClient3</strong></p></td>
<td align="left"><p><strong>m_Client3</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IDebugClient4</strong></p></td>
<td align="left"><p><strong>m_Client4</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IDebugClient5</strong></p></td>
<td align="left"><p><strong>m_Client5</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IDebugControl2</strong></p></td>
<td align="left"><p><strong>m_Control2</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IDebugControl3</strong></p></td>
<td align="left"><p><strong>m_Control3</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IDebugControl4</strong></p></td>
<td align="left"><p><strong>m_Control4</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IDebugData2</strong></p></td>
<td align="left"><p><strong>m_Data2</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IDebugData3</strong></p></td>
<td align="left"><p><strong>m_Data3</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IDebugData4</strong></p></td>
<td align="left"><p><strong>m_Data4</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IDebugRegisters2</strong></p></td>
<td align="left"><p><strong>m_Registers2</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IDebugSymbols2</strong></p></td>
<td align="left"><p><strong>m_Symbols2</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IDebugSymbols3</strong></p></td>
<td align="left"><p><strong>m_Symbols3</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IDebugSystemObjects2</strong></p></td>
<td align="left"><p><strong>m_System2</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><strong>IDebugSystemObjects3</strong></p></td>
<td align="left"><p><strong>m_System3</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><strong>IDebugSystemObjects4</strong></p></td>
<td align="left"><p><strong>m_System4</strong></p></td>
</tr>
</tbody>
</table>

 

在这些表中的成员进行初始化每次使用扩展库时要执行的扩展命令或格式输出的结构。 完成任务后，这些成员均未初始化。 因此，扩展不应缓存这些成员的值，并且应使用**ExtExtension**直接成员。

扩展库还可以创建自己的客户端使用该方法的对象[ **idebugclient:: Createclient** ](https://msdn.microsoft.com/library/windows/hardware/ff539320)或函数[ **DebugCreate** ](https://msdn.microsoft.com/library/windows/hardware/ff540469)或[ **DebugConnect**](https://msdn.microsoft.com/library/windows/hardware/ff540465)。

客户端对象的概述，请参阅[客户端对象](client-objects.md)。

 

 





