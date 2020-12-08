---
title: UEFI USB 功能协议
description: UEFI USB 功能协议
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b9e7005e973e43b3aefe7e1a7a52664a916e8526
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787993"
---
# <a name="uefi-usb-function-protocol"></a>UEFI USB 功能协议


**注意**   本节中的某些信息可能仅适用于 Windows 10 移动版和某些处理器体系结构。

 

USB 函数协议在 UEFI 环境中定义通用和轻型 USB 传输。 此协议由闪烁工具、USB 大容量存储模式和其他需要在启动到 UEFI 环境和主计算机的设备之间进行双向通信的工具使用。

## <a name="efi_usbfn_io_protocol"></a>EFI \_ USBFN \_ IO \_ 协议


与其他 UEFI 设备驱动程序一样，USB 函数驱动程序的入口点将 **efi \_ 驱动程序 \_ 绑定 \_ 协议** 附加到 **efi \_ USBFN \_ IO \_ 协议** 驱动程序的图像句柄

驱动程序绑定协议包含三个服务： " **支持**"、" **启动**" 和 " **停止**"。 **支持** 的函数必须进行测试，以查看此驱动程序是否支持给定的控制器。 **启动** 函数必须提供 USB 控制器的电源，如有必要，初始化硬件和内部数据结构，然后返回。 此函数不得激活该端口。 **Stop** 函数必须通过重置运行/停止位并关闭 USB 控制器（如果需要）来禁用设备。

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

**协议接口结构**

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

<a href="" id="revision"></a>**A01**  
**EFI \_ USBFN \_ IO \_ 协议** 遵循的修订版本。 所有将来的修订版都必须是向后兼容。 如果未来版本不是向后兼容的，则必须使用不同的 GUID。

<a href="" id="detectport"></a>**DetectPort**  
返回有关 USB 端口类型的信息。 请参阅 [EFI \_ USBFN \_ IO \_ 协议。DetectPort](efi-usbfn-io-protocoldetectport.md)。

<a href="" id="configureenableendpoints"></a>**ConfigureEnableEndpoints**  
基于提供的设备和配置描述符初始化所有终结点。 通过设置运行/停止位来启用设备。 请参阅 [EFI \_ USBFN \_ IO \_PROTOCOL.ConfigureEnableEndpoints](efi-usbfn-io-protocolconfigureenableendpoints.md)。

<a href="" id="getendpointmaxpacketsize"></a>**GetEndpointMaxPacketSize**  
返回指定终结点的最大数据包大小。 请参阅 [EFI \_ USBFN \_ IO \_ 协议。GetEndpointMaxPacketSize](efi-usbfn-io-protocolgetendpointmaxpacketsize.md)。

<a href="" id="getdeviceinfo"></a>**GetDeviceInfo**  
基于提供的标识符以 Unicode 字符串的形式返回特定于设备的信息。 请参阅 [EFI \_ USBFN \_ IO \_ 协议。GetDeviceInfo](efi-usbfn-io-protocolgetdeviceinfo.md)。

<a href="" id="getvendoridproductid"></a>**GetVendorIdProductId**  
返回设备的供应商 id 和产品 id。 请参阅 [EFI \_ USBFN \_ IO \_ 协议。GetVendorIdProductId](efi-usbfn-io-protocolgetvendoridproductid.md)。

<a href="" id="aborttransfer"></a>**AbortTransfer**  
在指定终结点上中止传输。 请参阅 [EFI \_ USBFN \_ IO \_ 协议。AbortTransfer](efi-usbfn-io-protocolaborttransfer.md)。

<a href="" id="getendpointstallstate"></a>**GetEndpointStallState**  
返回指定终结点上的延迟状态。 请参阅 [EFI \_ USBFN \_ IO \_ 协议。GetEndpointStallState](efi-usbfn-io-protocolgetendpointstallstate.md)。

<a href="" id="setendpointstalls"></a>**SetEndpointStallS**  
设置或清除指定终结点上的延迟状态。 请参阅 [EFI \_ USBFN \_ IO \_ 协议。SetEndpointStallState](efi-usbfn-io-protocolsetendpointstallstate.md)。

<a href="" id="eventhandler"></a>**EventHandler**  
重复调用此函数以接收有关 USB 总线状态的更新、接收、传输终结点上的完成事件以及终结点0上的安装包。 请参阅 [EFI \_ USBFN \_ IO \_ 协议。EventHandler](efi-usbfn-io-protocoleventhandler.md)。

<a href="" id="transfer"></a>**转换**  
此函数根据指定的方向，处理与指定终结点上的主机之间的数据传输。 请参阅 [EFI \_ USBFN \_ IO \_ 协议。传输](efi-usbfn-io-protocoltransfer.md)。

<a href="" id="getmaxtransfersize"></a>**GetMaxTransferSize**  
支持的最大传输大小（以字节为单位）。 请参阅 [EFI \_ USBFN \_ IO \_ 协议。GetMaxTransferSize](efi-usbfn-io-protocolgetmaxtransfersize.md)。

<a href="" id="allocatetransferbuffer"></a>**AllocateTransferBuffer**  
分配指定大小的传输缓冲区，该缓冲区满足控制器要求。 请参阅 [EFI \_ USBFN \_ IO \_ 协议。AllocateTransferBuffer](efi-usbfn-io-protocolallocatetransferbuffer.md)。

<a href="" id="freetransferbuffer"></a>**FreeTransferBuffer**  
取消分配通过 **AllocateTransferBuffer** 函数分配给传输缓冲区的内存。 请参阅 [EFI \_ USBFN \_ IO \_ 协议。FreeTransferBuffer](efi-usbfn-io-protocolfreetransferbuffer.md)。

<a href="" id="startcontroller"></a>**StartController**  
如果需要，请提供 USB 控制器的电源，并初始化硬件和内部数据结构。 请参阅 [EFI \_ USBFN \_ IO \_ 协议。StartController](efi-usbfn-io-protocolstartcontroller.md)。 此功能从协议的修订版0x00010001 开始可用。

<a href="" id="stopcontroller"></a>**StopController**  
通过重置运行/停止位来禁用设备，并在需要时关闭 USB 控制器。 请参阅 [EFI \_ USBFN \_ IO \_ 协议。StopController](efi-usbfn-io-protocolstopcontroller.md)。 此功能从协议的修订版0x00010001 开始可用。

<a href="" id="setendpointpolicy"></a>**SetEndpointPolicy**  
为指定的非控件终结点设置配置策略。 请参阅 [EFI \_ USBFN \_ IO \_ 协议。SetEndpointPolicy](efi-usbfn-io-protocolsetendpointpolicy.md)。 此功能从协议的修订版0x00010001 开始可用。

<a href="" id="getendpointpolicy"></a>**GetEndpointPolicy**  
检索指定的非控制终结点的配置策略。 请参阅 [EFI \_ USBFN \_ IO \_ 协议。GetEndpointPolicy](efi-usbfn-io-protocolgetendpointpolicy.md)。 此功能从协议的修订版0x00010001 开始可用。

<a href="" id="configureenableendpointsex"></a>**ConfigureEnableEndpointsEx**  
通过选择具有最高速度的设备和配置描述符 (最高) 硬件支持的 SuperSpeed。 通过设置运行/停止位启用设备。 请参阅 [EFI \_ USBFN \_ IO \_PROTOCOL.ConfigureEnableEndpointsEx](efi-usbfn-io-protocol-configureenableendpointsex.md)。 此功能从协议的修订版0x00010002 开始可用。

### <a name="remarks"></a>备注

下表列出了每个版本的 **EFI \_ USBFN \_ IO \_ 协议** 协议支持的函数。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>修订0x00010002</th>
<th>修订0x00010001</th>
<th>修订0x00010000</th>
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
<p><strong>转移</strong></p>
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
<p><strong>转移</strong></p>
<p><strong>GetMaxTransferSize</strong></p>
<p><strong>AllocateTransferBuffer</strong></p>
<p><strong>FreeTransferBuffer</strong></p></td>
</tr>
</tbody>
</table>
