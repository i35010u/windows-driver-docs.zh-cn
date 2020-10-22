---
description: 本主题介绍 USB 3.0 驱动程序堆栈的 USB 客户端驱动程序验证器功能，该功能使客户端驱动程序能够测试某些故障情况。
title: USB 客户端驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f9a0303402a1f77800e089c1e8ad03466374acac
ms.sourcegitcommit: a866b3470025d85b25a48857a81f893179698e7e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/22/2020
ms.locfileid: "92355969"
---
# <a name="usb-client-driver-verifier"></a>USB 客户端驱动程序验证程序

本主题介绍 USB 3.0 驱动程序堆栈的 USB 客户端驱动程序验证器功能，该功能使客户端驱动程序能够测试某些故障情况。

- [什么是 USB 客户端驱动程序验证程序](#what-is-the-usb-client-driver-verifier)
- [如何启用 USB 客户端驱动程序验证程序](#how-to-enable-the-usb-client-driver-verifier)
- [USB 客户端驱动程序验证程序的配置设置](#configuration-settings-for-the-usb-client-driver-verifier)

## <a name="what-is-the-usb-client-driver-verifier"></a>什么是 USB 客户端驱动程序验证程序

*Usb 客户端驱动程序验证*程序是包含在 Windows 8 中的 usb 3.0 驱动程序堆栈的一项功能。 当启用验证程序时，USB 驱动程序堆栈会失败或修改客户端驱动程序执行的某些操作。 这些故障将模拟可能难以找到的错误情况，并可能在以后导致不需要的结果。 模拟故障使你有机会确保你的驱动程序能够正常处理故障。 客户端可以通过错误处理代码处理错误，或使用不同的代码路径。

例如，客户端驱动程序支持通过大容量终结点的静态流进行的 i/o 操作。 通过使用验证程序，可以确保驱动程序的流逻辑正常工作，而不考虑各种主机控制器支持的流数量。 若要模拟这种情况，可以使用以后)  (讨论的 **UsbVerifierStaticStreamCountOverride** 设置。 当驱动程序每次调用 [**USBD \_ QueryUsbCapability**](/previous-versions/windows/hardware/drivers/hh406230(v=vs.85)) 来确定宿主控制器支持的静态流的最大数目时，例程将返回不同的值。

**重要提示**  USB 客户端驱动程序验证器仅针对各种 xHCI 控制器测试驱动程序。 它模拟了某些固有的2.0 控制器行为，如缺少链式 MDL 支持。 但是，我们建议你必须使用 USB 2.0 控制器测试你的客户端驱动程序，而不是使用此工具替换相同的。

Windows 硬件认证工具包包含运行模拟测试事例的自动测试。 有关详细信息，请参阅 [USB (USBDEX) 验证程序测试](https://docs.microsoft.com/previous-versions/windows/hardware/hck/hh998558(v=vs.85))。

## <a name="how-to-enable-the-usb-client-driver-verifier"></a>如何启用 USB 客户端驱动程序验证程序

若要使用 USB 客户端驱动程序验证程序，请在运行 Windows 8 的目标计算机上启用它。 目标计算机必须具有连接了 USB 设备的 xHCI 控制器。

当你为客户端驱动程序启用 [驱动程序验证程序](../devtest/driver-verifier.md) 时，将自动启用 "USB 客户端驱动程序验证程序"。 或者，您可以通过设置此注册表项来启用验证程序。

> [!NOTE]
> 启用 [Windows Driver Foundation (WDF) 验证器控件应用程序 ( # A0) ](/windows-hardware/drivers/devtest/wdf-verifier-control-application) 不会自动启用 USB 客户端驱动程序验证程序。

```cpp
HKEY_LOCAL_MACHINE
   SYSTEM
      CurrentControlSet
         services
            <Client Driver>
               Parameters
                  UsbVerifierEnabled (DWORD)
```

**UsbVerifierEnabled**注册表项采用 DWORD 值。 当 **UsbVerifierEnabled** 为1时，将启用 USB 客户端驱动程序验证程序;0禁用该方法。 如果为客户端驱动程序启用了 [驱动程序验证程序](../devtest/driver-verifier.md) ，并且 **UsbVerifierEnabled** 为0，则将禁用 USB 客户端驱动程序验证程序。

## <a name="configuration-settings-for-the-usb-client-driver-verifier"></a>USB 客户端驱动程序验证程序的配置设置

如果启用了验证程序，则 USB 驱动程序堆栈将跟踪客户端驱动程序通过调用 **USBD \_ xxxUrbAllocate** 例程分配的 URBs， (请参阅 [USB 例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/_usbref/#client)) 。 如果客户端驱动程序泄漏了任何 URB，则 USB 驱动程序堆栈会使用该信息通过 [Driver Verifier](https://docs.microsoft.com/windows-hardware/drivers/devtest/driver-verifier)来导致错误检查。 在这种情况下，请使用 **！ usbanalyze-v** 命令确定泄漏的原因。

此外，还可以配置 USB 客户端驱动程序验证程序，以修改或失败特定例程，并指定例程必须失败的频率。 若要配置验证程序，请按如下所示设置注册表项：

```cpp
HKEY_LOCAL_MACHINE
   SYSTEM
      CurrentControlSet
         services
            <Client driver>
               Parameters
                  <USB client driver verifier setting> (DWORD)
```

* &lt; USB 客户端驱动程序验证 &gt; 程序设置*注册表项采用 DWORD 值。
如果添加、修改或删除任何设置，则必须在系统中重新枚举设备以应用设置。

下表显示了 " * &lt; USB 客户端驱动程序验证程序 &gt; " 设置*的可能值。 这些设置应用于 " **服务** " 项下指定的客户端驱动程序。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>USB 客户端驱动程序验证程序设置</th>
<th>选择以下可能的值之一：</th>
<th>使用模拟 .。。</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>UsbVerifierFailRegistration</strong></p>
<p>客户端驱动程序对这些例程的调用失败：</p>
<ul>
<li><a href="/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceCreateWithParameters&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicecreatewithparameters)"><strong>WdfUsbTargetDeviceCreateWithParameters</strong></a></li>
<li><a href="/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle" data-raw-source="[&lt;strong&gt;USBD_CreateHandle&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle)"><strong>USBD_CreateHandle</strong></a></li>
</ul></td>
<td><ul>
<li>0：已禁用设置。</li>
<li>1：调用始终失败。</li>
<li><em>N</em>：调用失败，概率为 1/<em>N</em>，其中 <em>N</em> 是介于1到0x7FF 之间的十六进制值。 例如，如果 <em>N</em> 为10。 每10次调用都将失败。</li>
</ul></td>
<td><p><strong>客户端驱动程序注册失败。</strong></p>
<p>客户端驱动程序的其中一个初始化任务是向基础驱动程序堆栈注册自身。 接下来的几个调用中需要注册。</p>
<p>例如，客户端驱动程序调用 <a href="/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle" data-raw-source="[&lt;strong&gt;USBD_CreateHandle&lt;/strong&gt;](/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle)"><strong>USBD_CreateHandle</strong></a> 进行注册。 假设驱动程序假设例程始终返回 STATUS_SUCCESS，而不实现代码来处理失败。 如果例程返回错误 NTSTATUS 代码，驱动程序可能会无意中忽略该错误，并使用无效的 USBD 句柄继续执行后续调用。</p>
<p>设置允许您对调用失败，以便您可以测试故障代码路径。</p>
<p>注册失败时预期的客户端驱动程序行为：</p>
<ul>
<li><p>驱动程序不应继续正常工作。</p></li>
<li><p>该驱动程序不能导致系统崩溃，也不能通过选择忽略此故障而变得无响应。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>UsbVerifierFailChainedMdlSupport</strong></p>
<p>如果调用方将 GUID_USB_CAPABILITY_CHAINED_MDLS 传入 <em>CapabilityType</em> 参数，则客户端驱动程序对这些例程的调用将失败。</p>
<ul>
<li><a href="/previous-versions/windows/hardware/drivers/hh406230(v=vs.85)" data-raw-source="[&lt;strong&gt;USBD_QueryUsbCapability&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))"><strong>USBD_QueryUsbCapability</strong></a></li>
<li><a href="/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceQueryUsbCapability&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)"><strong>WdfUsbTargetDeviceQueryUsbCapability</strong></a></li>
</ul></td>
<td><ul>
<li>0：已禁用设置。</li>
<li>1：调用始终失败。</li>
<li><em>N</em>：调用失败，概率为 1/<em>N</em>，其中 <em>N</em> 是介于1到0x7FF 之间的十六进制值。 例如，如果 <em>N</em> 为10。 每10次调用都将失败。</li>
</ul></td>
<td><p><strong>与不支持链接 MDLs 的主机控制器通信。</strong></p>
<p>为了使客户端驱动程序发送链式 MDLs (参阅 <a href="/windows-hardware/drivers/kernel/using-mdls" data-raw-source="[MDL](../kernel/using-mdls.md)">MDL</a>) ，USB 驱动程序堆栈和主机控制器必须支持它们。</p>
<p>此设置允许你测试客户端驱动程序向连接到不支持的主机控制器的设备发送链式 MDL 请求时所执行的代码。 无论主机控制器是否支持链接的 MDLs，调用都会失败。</p>
<p>有关 USB 驱动程序堆栈中链接的 MDLs 支持的详细信息，请参阅 <a href="how-to-send-chained-mdls.md" data-raw-source="[How to Send Chained MDLs](how-to-send-chained-mdls.md)">如何发送链式 MDLs</a>。</p>
<p>当主机控制器不支持链接的 MDLs 时，预期的客户端驱动程序行为：</p>
<ul>
<li><p>该驱动程序应在不使用链式 MDLs 的情况下继续执行 i/o 传输。 这样，你还可以确保你的驱动程序适用于 USB 2.0 主机控制器，因为这些控制器不支持链接 MDLs。</p></li>
<li><p>该驱动程序不能导致系统崩溃，也不能通过选择忽略此故障而变得无响应。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>UsbVerifierFailStaticStreamsSupport</strong></p>
<p>如果调用方将 GUID_USB_CAPABILITY_STATIC_STREAMS 传入 <em>CapabilityType</em> 参数，则客户端驱动程序对这些例程的调用将失败。</p>
<ul>
<li><a href="/previous-versions/windows/hardware/drivers/hh406230(v=vs.85)" data-raw-source="[&lt;strong&gt;USBD_QueryUsbCapability&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))"><strong>USBD_QueryUsbCapability</strong></a></li>
<li><a href="/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceQueryUsbCapability&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)"><strong>WdfUsbTargetDeviceQueryUsbCapability</strong></a></li>
</ul></td>
<td><ul>
<li>0：已禁用设置。</li>
<li>1：调用始终失败。</li>
<li><em>N</em>：调用失败，概率为 1/<em>N</em>，其中 <em>N</em> 是介于1到0x7FF 之间的十六进制值。 例如，如果 <em>N</em> 为10。 每10次调用后，调用将失败。</li>
</ul></td>
<td><p><strong>与不支持静态流的主机控制器通信。</strong></p>
<p>为了使客户端驱动程序能够通过大容量终结点的静态流发送 i/o 传输，主机控制器必须支持流。</p>
<p>如果设备连接到不支持流的主机控制器，并且驱动程序尝试执行流 i/o 传输，则这些传输将失败。 此设置允许您在发生此类故障时测试代码。</p>
<p>当主机控制器不支持静态流时，预期的客户端驱动程序行为：</p>
<ul>
<li><p>如果客户端驱动程序要使用不支持流的 xHCI 控制器，则设备必须能够在不使用启用流的大容量终结点的情况下正常工作。</p></li>
<li><p>该驱动程序不能导致系统崩溃，也不能通过选择忽略此故障而变得无响应。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>UsbVerifierStaticStreamCountOverride</strong></p>
当客户端通过 GUID_USB_CAPABILITY_STATIC_STREAMS 调用这些例程时，更改 <em>OutputBuffer</em> 参数中接收的值。
<ul>
<li><a href="/previous-versions/windows/hardware/drivers/hh406230(v=vs.85)" data-raw-source="[&lt;strong&gt;USBD_QueryUsbCapability&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))"><strong>USBD_QueryUsbCapability</strong></a></li>
<li><a href="/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceQueryUsbCapability&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)"><strong>WdfUsbTargetDeviceQueryUsbCapability</strong></a></li>
</ul>
<p><em>OutputBuffer</em>值指示宿主控制器支持的静态流的最大数目。</p></td>
<td><ul>
<li>0：已禁用设置。</li>
<li>1：验证程序随机选择 <em>OutputBuffer</em> 值。 此值可用于进行压力测试，因为 <em>OutputBuffer</em> 值不重复，并且调用被测试的变体更多。</li>
<li><p><em>N</em>：指定 <em>OutputBuffer</em> 值。</p>
<p>如果启用了 <em>n</em> 值标志，则 <em>n</em> 必须小于 USB 驱动程序堆栈支持的最大流数。 因此，在设置此标志之前，必须通过成功的调用检索实际值。</p>
<p>如果 <em>N</em> 大于流的最大数目，则忽略此设置。</p></li>
</ul></td>
<td><p><strong>与各种主机控制器通信，每个控制器支持最大流数的不同值。</strong></p>
<p>通过使用此设置，可以确保无论各种主机控制器支持多少个流，驱动程序的流逻辑都有效。</p>
<p>可用于 i/o 传输的流的数量将受到主机控制器支持的流数的限制。</p>
<p>有关如何在客户端驱动程序中支持静态流的信息，请参阅 <a href="how-to-open-streams-in-a-usb-endpoint.md" data-raw-source="[How to Open and Close Static Streams in a USB Bulk Endpoint](how-to-open-streams-in-a-usb-endpoint.md)">如何在 USB 大容量终结点中打开和关闭静态流</a>。</p>
<p>当主机控制器支持的流数少于终结点时，预期的客户端驱动程序行为：</p>
<ul>
<li><p>客户端驱动程序可以选择以较少数量的流执行数据传输。</p></li>
<li><p>该驱动程序不能导致系统崩溃，也不能通过选择忽略此故障而变得无响应。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>UsbVerifierFailEnableStaticStreams</strong></p>
<p>将客户端驱动程序的打开的静态流请求 (URB_FUNCTION_OPEN_STATIC_STREAMS) 失败。</p></td>
<td><ul>
<li>0：已禁用设置。</li>
<li>1：请求始终失败。</li>
<li><em>N</em>：请求失败，概率为 1/<em>N</em>，其中 <em>N</em> 是介于1到0x7FF 之间的十六进制值。 例如，如果 <em>N</em> 为10。 每10次调用，请求会失败。</li>
</ul>
<div class="alert">
<strong>注意</strong>  如果先前对 <a href="/previous-versions/windows/hardware/drivers/hh406230(v=vs.85)" data-raw-source="[&lt;strong&gt;USBD_QueryUsbCapability&lt;/strong&gt;](/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))"><strong>USBD_QueryUsbCapability</strong></a> 或 <a href="/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceQueryUsbCapability&lt;/strong&gt;](/windows-hardware/drivers/ddi/wdfusb/nf-wdfusb-wdfusbtargetdevicequeryusbcapability)"><strong>WdfUsbTargetDeviceQueryUsbCapability</strong></a> 的调用失败，则打开的静态流请求会失败。
</div>
<div>
 
</div></td>
<td><p><strong>与支持静态流但请求因其他原因而失败的主机控制器通信。</strong></p>
<p>例如，你的设备连接到支持流的主机控制器。 客户端驱动程序发送一个打开的流请求，其中包含大量 (的流，以打开超出主机控制器所支持的最大流数量的) 。 USB 驱动程序堆栈将无法通过此类请求。</p>
<p>通过使用此设置，你可以测试打开流请求失败的错误处理代码。</p>
<p>当打开流请求失败时，预期的客户端驱动程序行为：</p>
<ul>
<li><p>驱动程序不应继续正常工作。</p></li>
<li><p>该驱动程序不能导致系统崩溃，也不能通过选择忽略此故障而变得无响应。</p></li>
</ul></td>
</tr>
</tbody>
</table>

## <a name="related-topics"></a>相关主题

[**USBD \_ CreateHandle**](https://docs.microsoft.com/windows-hardware/drivers/ddi/usbdlib/nf-usbdlib-usbd_createhandle)  
[**USBD \_ QueryUsbCapability**](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/hh406230(v=vs.85))  
[如何在 USB 批量终结点中打开和关闭静态流](how-to-open-streams-in-a-usb-endpoint.md)  
[如何发送链式 MDLs](how-to-send-chained-mdls.md)  
[Microsoft USB 测试工具 (MUTT) 设备的概述](/windows-hardware/drivers/usbcon/microsoft-usb-test-tool--mutt--devices)
