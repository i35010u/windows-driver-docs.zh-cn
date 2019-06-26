---
title: 客户端对象和引擎
description: 客户端对象和引擎
ms.assetid: 959912c0-bce9-4d5b-9119-1ac07a8ea1ad
keywords:
- EngExtCpp 扩展，客户端对象
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: a0780c269b9c3d4121b811ca36ebd6d804cf51ca
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67361464"
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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugadvanced" data-raw-source="[IDebugAdvanced](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugadvanced)">IDebugAdvanced</a></p></td>
<td align="left"><p><strong>m_Advanced</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugclient" data-raw-source="[IDebugClient](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugclient)">IDebugClient</a></p></td>
<td align="left"><p><strong>m_Client</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugcontrol" data-raw-source="[IDebugControl](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugcontrol)">IDebugControl</a></p></td>
<td align="left"><p><strong>m_Control</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugdataspaces" data-raw-source="[IDebugDataSpaces](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugdataspaces)">IDebugDataSpaces</a></p></td>
<td align="left"><p><strong>m_Data</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugregisters" data-raw-source="[IDebugRegisters](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugregisters)">IDebugRegisters</a></p></td>
<td align="left"><p><strong>m_Registers</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugsymbols" data-raw-source="[IDebugSymbols](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugsymbols)">IDebugSymbols</a></p></td>
<td align="left"><p><strong>m_Symbols</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugsystemobjects" data-raw-source="[IDebugSystemObjects](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nn-dbgeng-idebugsystemobjects)">IDebugSystemObjects</a></p></td>
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

扩展库还可以创建自己的客户端使用该方法的对象[ **idebugclient:: Createclient** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-idebugclient5-createclient)或函数[ **DebugCreate** ](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-debugcreate)或[ **DebugConnect**](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/dbgeng/nf-dbgeng-debugconnect)。

客户端对象的概述，请参阅[客户端对象](client-objects.md)。

 

 





