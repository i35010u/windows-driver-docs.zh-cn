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
ms.openlocfilehash: 7d988c24da7e532ff37f441dd2a87be21418430a
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72837542"
---
# <a name="querying-for-bluetooth-interfaces"></a>查询蓝牙接口


蓝牙驱动程序堆栈公开了以下接口，配置文件驱动程序可以使用这些接口来与蓝牙设备交互。

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
<td align="left"><p>配置文件驱动程序查询 GUID_BTHDDI_SDP_NODE_INTERFACE 获取指向允许它们创建服务发现协议（SDP）记录的函数的指针。</p>
<p>此接口与<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_node_interface" data-raw-source="[&lt;strong&gt;BTHDDI_SDP_NODE_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_node_interface)"><strong>BTHDDI_SDP_NODE_INTERFACE</strong></a>结构相对应。</p></td>
</tr>
<tr class="even">
<td align="left"><p>GUID_BTHDDI_SDP_PARSE_INTERFACE</p></td>
<td align="left"><p>配置文件驱动程序查询 GUID_BTHDDI_SDP_PARSE_INTERFACE 以获取指向允许其分析 SDP 记录的函数的指针。</p>
<p>此接口与<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_parse_interface" data-raw-source="[&lt;strong&gt;BTHDDI_SDP_PARSE_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthsdpddi/ns-bthsdpddi-_bthddi_sdp_parse_interface)"><strong>BTHDDI_SDP_PARSE_INTERFACE</strong></a>结构相对应。</p></td>
</tr>
<tr class="odd">
<td align="left"><p>GUID_BTHDDI_PROFILE_DRIVER_INTERFACE</p></td>
<td align="left"><p>配置文件驱动程序查询 BTHDDI_PROFILE_DRIVER_INTERFACE 以获取指向允许其创建、分配、重用和免费 BRBs 的函数的指针。</p>
<p>此接口与<a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_bth_profile_driver_interface" data-raw-source="[&lt;strong&gt;BTH_PROFILE_DRIVER_INTERFACE&lt;/strong&gt;](https://docs.microsoft.com/windows-hardware/drivers/ddi/bthddi/ns-bthddi-_bth_profile_driver_interface)"><strong>BTH_PROFILE_DRIVER_INTERFACE</strong></a>结构相对应。</p></td>
</tr>
</tbody>
</table>

 

若要获取这些接口中的任何一个，配置文件驱动程序必须首先构建[**IRP\_MN\_QUERY\_INTERFACE**](https://docs.microsoft.com/windows-hardware/drivers/kernel/irp-mn-query-interface) irp 发送到蓝牙驱动程序堆栈。

下面的过程是获取其中一个接口的一般过程。

### <a name="span-idto_query_for_an_interfacespanspan-idto_query_for_an_interfacespanto-query-for-an-interface"></a><span id="to_query_for_an_interface"></span><span id="TO_QUERY_FOR_AN_INTERFACE"></span>查询接口

1.  分配并初始化 IRP。

2.  分配并初始化接口的实例。

3.  指定主要和次要函数代码以查询接口。

4.  指定要查询的接口。

5.  将 IRP 向下传递到要处理的驱动程序堆栈。

下面的伪代码示例演示如何设置 IRP\_MN\_QUERY\_INTERFACE IRP，以查询 GUID 的蓝牙驱动程序堆栈\_BTHDDI\_\_DRIVER\_INTERFACE。

  **请注意**，为了提高可读性，下面的伪代码示例不演示错误处理。

 

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

如果 IRP 成功返回，则配置文件驱动程序可以访问和使用接口中包含的函数指针。

 

 





