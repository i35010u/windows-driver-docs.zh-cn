---
title: 查询蓝牙接口
description: 查询蓝牙接口
ms.assetid: 56db29cd-26ab-4262-9b9f-40d46372ffe9
keywords:
- 蓝牙 WDK，接口查询
- 查询蓝牙接口
- 接口 WDK 蓝牙
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e80cd3d00cb30abf85ab3aaffcc4ff9418447fa3
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67354002"
---
# <a name="querying-for-bluetooth-interfaces"></a>查询蓝牙接口


蓝牙驱动程序堆栈公开以下配置文件驱动程序可用于与蓝牙设备交互的接口。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">接口</th>
<th align="left">描述</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>GUID_BTHDDI_SDP_NODE_INTERFACE</p></td>
<td align="left"><p>GUID_BTHDDI_SDP_NODE_INTERFACE 以获取指向函数，以便创建服务发现协议 (SDP) 记录的配置文件驱动程序查询。</p>
<p>此接口对应于<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_node_interface" data-raw-source="[&lt;strong&gt;BTHDDI_SDP_NODE_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_node_interface)"> <strong>BTHDDI_SDP_NODE_INTERFACE</strong> </a>结构。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GUID_BTHDDI_SDP_PARSE_INTERFACE</p></td>
<td align="left"><p>GUID_BTHDDI_SDP_PARSE_INTERFACE 以获取指向函数，以便分析 SDP 记录的配置文件驱动程序查询。</p>
<p>此接口对应于<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_parse_interface" data-raw-source="[&lt;strong&gt;BTHDDI_SDP_PARSE_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_parse_interface)"> <strong>BTHDDI_SDP_PARSE_INTERFACE</strong> </a>结构。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GUID_BTHDDI_PROFILE_DRIVER_INTERFACE</p></td>
<td align="left"><p>若要获取指向函数，以便创建、 分配、 重用和免费 BRBs BTHDDI_PROFILE_DRIVER_INTERFACE 的配置文件驱动程序查询。</p>
<p>此接口对应于<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_bth_profile_driver_interface" data-raw-source="[&lt;strong&gt;BTH_PROFILE_DRIVER_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/bthddi/ns-bthddi-_bth_profile_driver_interface)"> <strong>BTH_PROFILE_DRIVER_INTERFACE</strong> </a>结构。</p></td>
</tr>
</tbody>
</table>

 

若要获取任何这些接口，配置文件驱动程序必须首先生成并发送[ **IRP\_MN\_查询\_接口**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface) IRP 到蓝牙驱动程序堆栈。

以下步骤是获取这些接口的其中一个的一般过程。

### <a name="span-idtoqueryforaninterfacespanspan-idtoqueryforaninterfacespanto-query-for-an-interface"></a><span id="to_query_for_an_interface"></span><span id="TO_QUERY_FOR_AN_INTERFACE"></span>若要查询接口

1.  分配并初始化 IRP。

2.  分配并初始化接口的实例。

3.  指定要查询接口的主版本号和次函数代码。

4.  指定查询接口。

5.  通过向驱动程序堆栈下的 IRP，要处理。

下面的伪代码示例演示如何设置 IRP\_MN\_查询\_接口 IRP，若要查询的 GUID 的蓝牙驱动程序堆栈\_BTHDDI\_配置文件\_驱动程序\_接口。

**请注意**  以提高可读性，下面的伪代码示例并不演示错误处理。

 

```cpp
#include <bthddi.h>

...

// Define a custom pool tag to identify your profile driver's dynamic memory allocations. You should change this tag to easily identify your driver's allocations from other drivers.
#define PROFILE_DRIVER_POOL_TAG '_htB'

PIRP Irp;
Irp = IoAllocateIrp( DeviceExtension->ParentDeviceObject->StackSize, FALSE );

PBTH_PROFILE_DRIVER_INTERFACE BthInterface; // Define storage for an instance of the BTH_PROFILE_DRIVER_INTERFACE structure
BthInterface = ExAllocatePoolWithTag( NonPagedPool, sizeof( BTH_PROFILE_DRIVER_INTERFACE ), PROFILE_DRIVER_POOL_TAG );

// Zero the memory associated with the structure
RtlZeroMemory( BthInterface, sizeof( BTH_PROFILE_DRIVER_INTERFACE ) );

// Set up the next IRP stack location
PIO_STACK_LOCATION NextIrpStack;
NextIrpStack = IoGetNextIrpStackLocation( Irp );
NextIrpStack->MajorFunction = IRP_MJ_PNP;
NextIrpStack->MinorFunction = IRP_MN_QUERY_INTERFACE;
NextIrpStack->Parameters.QueryInterface.InterfaceType = (LPGUID) &GUID_BTHDDI_PROFILE_DRIVER_INTERFACE;
NextIrpStack->Parameters.QueryInterface.Size = sizeof( BTH_PROFILE_DRIVER_INTERFACE );
NextIrpStack->Parameters.QueryInterface.Version = BTHDDI_PROFILE_DRIVER_INTERFACE_VERSION_FOR_QI;
NextIrpStack->Parameters.QueryInterface.Interface = (PINTERFACE) BthInterface;
NextIrpStack->Parameters.QueryInterface.InterfaceSpecificData = NULL;

// Pass the IRP down the driver stack
NTSTATUS Status;
Status = IoCallDriver( DeviceExtension->NextLowerDriver, Irp );
```

如果 IRP 成功返回，则可以访问配置文件驱动程序然后将其使用界面中包含的函数指针。

 

 





