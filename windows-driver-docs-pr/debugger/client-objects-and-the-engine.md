---
title: 客户端对象和引擎
description: 客户端对象和引擎
ms.assetid: 959912c0-bce9-4d5b-9119-1ac07a8ea1ad
keywords:
- EngExtCpp 扩展，客户端对象
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: 376ad7ec4782f32087c53c63c062e21fcb6bb8c8
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212247"
---
# <a name="client-objects-and-the-engine"></a>客户端对象和引擎


## <span id="ddk_using_clients_and_the_engine_dbx"></span><span id="DDK_USING_CLIENTS_AND_THE_ENGINE_DBX"></span>


EngExtCpp 扩展通过客户端对象与 [调试器引擎](introduction.md#debugger-engine) 进行交互。 指向客户端对象的接口指针可通过 [**ExtExtension**](/previous-versions/ff543981(v=vs.85)) 基类的成员用于扩展。 以下成员提供对第一个版本的引擎 API 接口的访问权限。

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
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugadvanced" data-raw-source="[IDebugAdvanced](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugadvanced)">IDebugAdvanced</a></p></td>
<td align="left"><p><strong>m_Advanced</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugclient" data-raw-source="[IDebugClient](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugclient)">IDebugClient</a></p></td>
<td align="left"><p><strong>m_Client</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugcontrol" data-raw-source="[IDebugControl](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugcontrol)">IDebugControl</a></p></td>
<td align="left"><p><strong>m_Control</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugdataspaces" data-raw-source="[IDebugDataSpaces](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugdataspaces)">IDebugDataSpaces</a></p></td>
<td align="left"><p><strong>m_Data</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugregisters" data-raw-source="[IDebugRegisters](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugregisters)">IDebugRegisters</a></p></td>
<td align="left"><p><strong>m_Registers</strong></p></td>
</tr>
<tr class="even">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugsymbols" data-raw-source="[IDebugSymbols](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugsymbols)">IDebugSymbols</a></p></td>
<td align="left"><p><strong>m_Symbols</strong></p></td>
</tr>
<tr class="odd">
<td align="left"><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugsystemobjects" data-raw-source="[IDebugSystemObjects](/windows-hardware/drivers/ddi/dbgeng/nn-dbgeng-idebugsystemobjects)">IDebugSystemObjects</a></p></td>
<td align="left"><p><strong>m_System</strong></p></td>
</tr>
</tbody>
</table>

 

以下成员提供对更高版本的引擎 API 接口的访问权限。 这些接口在所有版本的调试器引擎中可能不可用。 如果它们不可用，则任何使用它们的尝试都将导致引发异常。

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

 

每次使用扩展库执行扩展命令或设置输出的结构的格式时，都会对这些表中的成员进行初始化。 任务完成后，这些成员未初始化。 因此，扩展不应缓存这些成员的值，而应直接使用 **ExtExtension** 成员。

扩展库还可以使用方法 [**IDebugClient：： CreateClient**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-idebugclient5-createclient) 或函数 [**DebugCreate**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-debugcreate) 或 [**DebugConnect**](/windows-hardware/drivers/ddi/dbgeng/nf-dbgeng-debugconnect)创建自己的客户端对象。

有关客户端对象的概述，请参阅 [客户端对象](client-objects.md)。

 

