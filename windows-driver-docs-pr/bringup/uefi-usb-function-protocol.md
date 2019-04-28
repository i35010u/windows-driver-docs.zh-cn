---
title: UEFI USB 功能协议
description: UEFI USB 功能协议
ms.assetid: eac35cf4-82b4-4d7e-ae69-8f506f12ae5d
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06f53d5ab7c43b9b1f7212f7cbb3df233d23c300
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63337365"
---
# <a name="uefi-usb-function-protocol"></a>UEFI USB 功能协议


**请注意**  本部分中的某些信息可能仅适用于 Windows 10 移动版和某些处理器体系结构。

 

USB 函数协议 UEFI 环境中定义的泛型和轻型 USB 传输。 此协议使用闪烁的工具、 USB 大容量存储模式和其他工具，需要启动到 UEFI 环境的设备和主机计算机之间的双向通信。

## <a name="efiusbfnioprotocol"></a>EFI\_USBFN\_IO\_协议


其他 UEFI 的设备驱动程序，如 USB 的入口点函数驱动程序附加**EFI\_驱动程序\_绑定\_协议**到的图像图柄**EFI\_USBFN\_IO\_协议**驱动程序

驱动程序绑定协议包含三个服务，**支持**，**启动**，并**停止**。 **支持**函数必须进行测试以查看此驱动程序是否支持给定的控制器。 **启动**函数必须提供为 USB 控制器，必要时，初始化硬件和内部数据结构，然后返回。 此函数，必须激活该端口。 **停止**函数必须通过重置运行/停止位和 USB 控制器关闭电源，如果需要禁用设备。

**GUID**

```cpp
// {32D2963A-FE5D-4f30-B633-6E5DC55803CC}
#define EFI_USBFN_IO_PROTOCOL_GUID \
  {0x32d2963a, 0xfe5d, 0x4f30, 0xb6, 0x33, 0x6e, 0x5d, 0xc5, \
   0x58, 0x3, 0xcc };
```

**修订号**

```cpp
#define EFI_USBFN_IO_PROTOCOL_REVISION   0x00010002
```

**协议的接口结构**

```cpp
typedef struct _EFI_USBFN_IO_PROTOCOL 
{
  UINT32                                      Revision;
  EFI_USBFN_IO_DETECT_PORT                    DetectPort;
  EFI_USBFN_IO_CONFIGURE_ENABLE_ENDPOINTS     ConfigureEnableEndpoints;
  EFI_USBFN_IO_GET_ENDPOINT_MAXPACKET_SIZE    GetEndpointMaxPacketSize;
  EFI_USBFN_IO_GET_DEVICE_INFO                GetDeviceInfo;
  EFI_USBFN_IO_GET_VENDOR_ID_PRODUCT_ID       GetVendorIdProductId;
  EFI_USBFN_IO_ABORT_TRANSFER                 AbortTransfer;
  EFI_USBFN_IO_GET_ENDPOINT_STALL_STATE       GetEndpointStallState; 
  EFI_USBFN_IO_SET_ENDPOINT_STALL_STATE       SetEndpointStallState;
  EFI_USBFN_IO_EVENTHANDLER                   EventHandler;
  EFI_USBFN_IO_TRANSFER                       Transfer;
  EFI_USBFN_IO_GET_MAXTRANSFER_SIZE           GetMaxTransferSize;
  EFI_USBFN_IO_ALLOCATE_TRANSFER_BUFFER       AllocateTransferBuffer;
  EFI_USBFN_IO_FREE_TRANSFER_BUFFER           FreeTransferBuffer;
  EFI_USBFN_IO_START_CONTROLLER               StartController;
  EFI_USBFN_IO_STOP_CONTROLLER                StopController;
  EFI_USBFN_IO_SET_ENDPOINT_POLICY            SetEndpointPolicy;
  EFI_USBFN_IO_GET_ENDPOINT_POLICY            GetEndpointPolicy;
  EFI_USBFN_IO_CONFIGURE_ENABLE_ENDPOINTS_EX  ConfigureEnableEndpointsEx;
} EFI_USBFN_IO_PROTOCOL;
```

### <a name="members"></a>成员

<a href="" id="revision"></a>**修订版本**  
修订**EFI\_USBFN\_IO\_协议**遵循。 所有未来的版本必须是向后兼容。 如果将来的版本不是向后兼容，必须使用不同的 GUID。

<a href="" id="detectport"></a>**DetectPort**  
返回有关 USB 端口类型信息。 请参阅[EFI\_USBFN\_IO\_协议。DetectPort](efi-usbfn-io-protocoldetectport.md)。

<a href="" id="configureenableendpoints"></a>**ConfigureEnableEndpoints**  
初始化基于提供的设备和配置描述符的所有终结点。 通过设置运行/停止位启用该设备。 请参阅[EFI\_USBFN\_IO\_协议。ConfigureEnableEndpoints](efi-usbfn-io-protocolconfigureenableendpoints.md)。

<a href="" id="getendpointmaxpacketsize"></a>**GetEndpointMaxPacketSize**  
返回指定的终结点的最大数据包大小。 请参阅[EFI\_USBFN\_IO\_协议。GetEndpointMaxPacketSize](efi-usbfn-io-protocolgetendpointmaxpacketsize.md)。

<a href="" id="getdeviceinfo"></a>**GetDeviceInfo**  
返回基于提供的标识符为 Unicode 字符串的设备特定信息。 请参阅[EFI\_USBFN\_IO\_协议。GetDeviceInfo](efi-usbfn-io-protocolgetdeviceinfo.md)。

<a href="" id="getvendoridproductid"></a>**GetVendorIdProductId**  
返回供应商 id 和设备的产品 id。 请参阅[EFI\_USBFN\_IO\_协议。GetVendorIdProductId](efi-usbfn-io-protocolgetvendoridproductid.md)。

<a href="" id="aborttransfer"></a>**AbortTransfer**  
指定终结点上传输中止。 请参阅[EFI\_USBFN\_IO\_协议。AbortTransfer](efi-usbfn-io-protocolaborttransfer.md)。

<a href="" id="getendpointstallstate"></a>**GetEndpointStallState**  
返回指定终结点上停止状态。 请参阅[EFI\_USBFN\_IO\_协议。GetEndpointStallState](efi-usbfn-io-protocolgetendpointstallstate.md)。

<a href="" id="setendpointstalls"></a>**SetEndpointStallS**  
设置或清除指定的终结点上的停止状态。 请参阅[EFI\_USBFN\_IO\_协议。SetEndpointStallState](efi-usbfn-io-protocolsetendpointstallstate.md)。

<a href="" id="eventhandler"></a>**EventHandler**  
重复调用此函数来接收有关 USB 总线状态更新、 接收、 传输终结点上的完成事件数和终结点 0 上的安装程序数据包。 请参阅[EFI\_USBFN\_IO\_协议。事件处理程序](efi-usbfn-io-protocoleventhandler.md)。

<a href="" id="transfer"></a>**传输**  
此函数处理传输数据到或从该主机上指定的终结点，具体取决于指定的方向。 请参阅[EFI\_USBFN\_IO\_协议。传输](efi-usbfn-io-protocoltransfer.md)。

<a href="" id="getmaxtransfersize"></a>**GetMaxTransferSize**  
受支持的最大传输大小 （字节）。 请参阅[EFI\_USBFN\_IO\_协议。GetMaxTransferSize](efi-usbfn-io-protocolgetmaxtransfersize.md)。

<a href="" id="allocatetransferbuffer"></a>**AllocateTransferBuffer**  
分配满足控制器要求指定大小的传输缓冲区。 请参阅[EFI\_USBFN\_IO\_协议。AllocateTransferBuffer](efi-usbfn-io-protocolallocatetransferbuffer.md)。

<a href="" id="freetransferbuffer"></a>**FreeTransferBuffer**  
取消分配的传输缓冲区分配的内存**AllocateTransferBuffer**函数。 请参阅[EFI\_USBFN\_IO\_协议。FreeTransferBuffer](efi-usbfn-io-protocolfreetransferbuffer.md)。

<a href="" id="startcontroller"></a>**StartController**  
如果需要提供为 USB 控制器并初始化硬件和内部数据结构。 请参阅[EFI\_USBFN\_IO\_协议。StartController](efi-usbfn-io-protocolstartcontroller.md)。 此函数是可以开始于修订 0x00010001 的协议。

<a href="" id="stopcontroller"></a>**StopController**  
通过重置运行/停止位和关闭 USB 控制器，如果需要禁用的设备。 请参阅[EFI\_USBFN\_IO\_协议。StopController](efi-usbfn-io-protocolstopcontroller.md)。 此函数是可以开始于修订 0x00010001 的协议。

<a href="" id="setendpointpolicy"></a>**SetEndpointPolicy**  
设置指定非控制终结点的配置策略。 请参阅[EFI\_USBFN\_IO\_协议。SetEndpointPolicy](efi-usbfn-io-protocolsetendpointpolicy.md)。 此函数是可以开始于修订 0x00010001 的协议。

<a href="" id="getendpointpolicy"></a>**GetEndpointPolicy**  
检索指定非控制终结点的配置策略。 请参阅[EFI\_USBFN\_IO\_协议。GetEndpointPolicy](efi-usbfn-io-protocolgetendpointpolicy.md)。 此函数是可以开始于修订 0x00010001 的协议。

<a href="" id="configureenableendpointsex"></a>**ConfigureEnableEndpointsEx**  
通过选择的设备和配置描述符 （最多 SuperSpeed) 最高速度的硬件支持的初始化的所有终结点。 允许设备通过设置运行/停止位。 请参阅[EFI\_USBFN\_IO\_协议。ConfigureEnableEndpointsEx](efi-usbfn-io-protocol-configureenableendpointsex.md)。 此函数是可以开始于修订 0x00010002 的协议。

### <a name="remarks"></a>备注

下表列出了支持的每个版本中的函数**EFI\_USBFN\_IO\_协议**协议。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>修订 0x00010002</th>
<th>修订 0x00010001</th>
<th>修订 0x00010000</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>ConfigureEnableEndpointsEx</strong></p></td>
<td><p><strong>DetectPort</strong></p>
<p><strong>ConfigureEnableEndpoints</strong></p>
<p><strong>GetEndpointMaxPacketSize</strong></p>
<p><strong>GetDeviceInfo</strong></p>
<p><strong>GetVendorIdProductId</strong></p>
<p><strong>AbortTransfer</strong></p>
<p><strong>GetEndpointStallState</strong></p>
<p><strong>SetEndpointStallState</strong></p>
<p><strong>EventHandler</strong></p>
<p><strong>传输</strong></p>
<p><strong>GetMaxTransferSize</strong></p>
<p><strong>AllocateTransferBuffer</strong></p>
<p><strong>FreeTransferBuffer</strong></p>
<p><strong>StartController</strong></p>
<p><strong>StopController</strong></p>
<p><strong>SetEndpointPolicy</strong></p>
<p><strong>GetEndpointPolicy</strong></p></td>
<td><p><strong>DetectPort</strong></p>
<p><strong>ConfigureEnableEndpoints</strong></p>
<p><strong>GetEndpointMaxPacketSize</strong></p>
<p><strong>GetDeviceInfo</strong></p>
<p><strong>GetVendorIdProductId</strong></p>
<p><strong>AbortTransfer</strong></p>
<p><strong>GetEndpointStallState</strong></p>
<p><strong>SetEndpointStallState</strong></p>
<p><strong>EventHandler</strong></p>
<p><strong>传输</strong></p>
<p><strong>GetMaxTransferSize</strong></p>
<p><strong>AllocateTransferBuffer</strong></p>
<p><strong>FreeTransferBuffer</strong></p></td>
</tr>
</tbody>
</table>
