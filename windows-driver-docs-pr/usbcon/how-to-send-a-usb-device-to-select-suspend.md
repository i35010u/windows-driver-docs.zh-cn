---
Description: 本主题介绍 USB 客户端驱动程序验证工具功能，客户端驱动程序来测试某些失败的情况下的 USB 3.0 驱动程序堆栈。
title: USB 客户端驱动程序验证程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9ad54348fd0c397e4a5fccca64cd86dea7fadefe
ms.sourcegitcommit: 0504cc497918ebb7b41a205f352046a66c0e26a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/08/2019
ms.locfileid: "65405042"
---
# <a name="usb-client-driver-verifier"></a>USB 客户端驱动程序验证程序


本主题介绍 USB 客户端驱动程序验证工具功能，客户端驱动程序来测试某些失败的情况下的 USB 3.0 驱动程序堆栈。

-   [USB 客户端驱动程序验证工具是什么](#what-is-the-usb-client-driver-verifier)
-   [如何启用 USB 客户端驱动程序验证工具](#how-to-enable-the-usb-client-driver-verifier)
-   [USB 客户端驱动程序验证程序的配置设置](#configuration-settings-for-the-usb-client-driver-verifier)

## <a name="what-is-the-usb-client-driver-verifier"></a>USB 客户端驱动程序验证工具是什么


*USB 客户端驱动程序验证工具*是一项功能包含在 Windows 8 的 USB 3.0 驱动程序堆栈。 启用验证工具后，USB 驱动程序堆栈失败或修改某些由客户端驱动程序执行的操作。 这些故障模拟错误条件的可能是否则很难查找和更高版本可能导致意外结果。 模拟的故障为您提供机会，以确保您的驱动程序能够正常处理失败。 客户端可以处理通过错误处理代码的错误或执行不同的代码路径。

例如，客户端驱动程序支持通过大容量终结点的静态流 I/O 操作。 通过使用验证器，可以确保该驱动程序的流处理逻辑的工作方式，而不考虑流支持的不同主机控制器的数量。 若要模拟这种情况下，可以使用**UsbVerifierStaticStreamCountOverride**设置 （稍后讨论）。 每次驱动程序调用[ **USBD\_QueryUsbCapability** ](https://msdn.microsoft.com/library/windows/hardware/hh406230)若要确定主机控制器支持的静态流的最大数目，例程将返回不同的值。

**重要**  USB 客户端驱动程序验证工具仅测试您的驱动程序针对各种 xHCI 控制器。 一些固有的 2.0 控制器行为，例如缺少链接 MDL 支持模拟。 但是，我们建议必须测试具有 USB 2.0 控制器在客户端驱动程序和不使用此工具来替换为相同。

 

Windows 硬件认证工具包包括自动的测试运行模拟的测试用例。 有关详细信息，请参阅[USB (USBDEX) 验证工具测试](https://msdn.microsoft.com/library/windows/hardware/hh998558.aspx)。

## <a name="how-to-enable-the-usb-client-driver-verifier"></a>如何启用 USB 客户端驱动程序验证工具


若要使用 USB 客户端驱动程序验证工具，您的目标计算机上的正在运行的 Windows 8 上启用它。 目标计算机必须具有 USB 设备连接到的 xHCI 控制器。

启用时，会自动启用 USB 客户端驱动程序验证工具[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)客户端驱动程序。 或者，您可以通过设置此注册表项来启用验证程序。

**请注意**  启用[Windows Driver Foundation (WDF) 验证程序控件应用程序 (WdfVerifier.exe)](https://msdn.microsoft.com/library/windows/hardware/ff556129)不会自动启用 USB 客户端驱动程序验证工具。

 

```cpp
HKEY_LOCAL_MACHINE
   SYSTEM
      CurrentControlSet
         services
            <Client Driver>
               Parameters
                  UsbVerifierEnabled (DWORD)
```

**UsbVerifierEnabled**注册表条目采用 DWORD 值。 当**UsbVerifierEnabled**为 1，USB 客户端驱动程序验证工具，则启用; 0 禁用它。 如果[Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)启用了客户端驱动程序和**UsbVerifierEnabled**为 0，则禁用 USB 客户端驱动程序验证工具。

## <a name="configuration-settings-for-the-usb-client-driver-verifier"></a>USB 客户端驱动程序验证程序的配置设置


启用验证工具后，会跟踪 USB 驱动程序堆栈的客户端驱动程序将通过调用其分配的 URBs **USBD\_xxxUrbAllocate**例程 (请参阅[USB 例程](https://docs.microsoft.com/windows-hardware/drivers/ddi/content/_usbref/#client))。 如果客户端驱动程序泄漏任何 URB、 USB 驱动程序堆栈使用该信息会导致通过出现 bugcheck [Driver Verifier](https://msdn.microsoft.com/library/windows/hardware/ff545448)。 在这种情况下，使用 **！ usbanalyze v**命令，以确定泄露的原因。

此外，（可选） 你可以配置 USB 客户端驱动程序验证工具来修改或失败特定的例程，并指定何种频率例程时不能。 若要配置验证程序，请设置注册表项，如下所示：

```cpp
HKEY_LOCAL_MACHINE
   SYSTEM
      CurrentControlSet
         services
            <Client driver>
               Parameters
                  <USB client driver verifier setting> (DWORD)
```

 *&lt;USB 客户端驱动程序验证工具设置&gt;* 注册表条目采用 DWORD 值。
如果您添加、 修改或删除任何设置，必须重新枚举系统以应用设置的设备。

此表显示了可能的值为 *&lt;USB 客户端驱动程序验证工具设置&gt;*。 设置适用于下指定的客户端驱动程序**services**密钥。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>USB 客户端驱动程序验证程序设置</th>
<th>选择以下可能值之一：</th>
<th>使用模拟...</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>UsbVerifierFailRegistration</strong></p>
<p>对这些例程的客户端驱动程序的调用将失败：</p>
<ul>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh439428" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceCreateWithParameters&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439428)"><strong>WdfUsbTargetDeviceCreateWithParameters</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh406241" data-raw-source="[&lt;strong&gt;USBD_CreateHandle&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406241)"><strong>USBD_CreateHandle</strong></a></li>
</ul></td>
<td><ul>
<li>0:设置处于禁用状态。</li>
<li>1：调用将始终失败。</li>
<li><em>N</em>:调用将失败的概率为 1 /<em>N</em>，其中<em>N</em>是介于 1 到 0x7FF 之间的十六进制值。 例如，如果<em>N</em>为 10。 调用失败一次每个 10 次调用。</li>
</ul></td>
<td><p><strong>客户端驱动程序注册失败。</strong></p>
<p>客户端驱动程序的初始化任务之一是能够将自身注册基础驱动程序堆栈。 在多个后续调用中必须进行注册。</p>
<p>例如，客户端驱动程序调用<a href="https://msdn.microsoft.com/library/windows/hardware/hh406241" data-raw-source="[&lt;strong&gt;USBD_CreateHandle&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406241)"> <strong>USBD_CreateHandle</strong> </a>进行注册。 让我们假设驱动程序假定该例程始终返回 STATUS_SUCCESS，且不实现代码来处理失败。 如果例程将返回错误 NTSTATUS 代码，该驱动程序无意中可以忽略错误并继续进行后续调用使用 USBD 句柄无效。</p>
<p>设置，以便可以测试失败可代码路径失败的调用。</p>
<p>注册失败时预期的客户端驱动程序行为：</p>
<ul>
<li><p>该驱动程序不应继续照常工作。</p></li>
<li><p>该驱动程序不得导致系统崩溃或通过选择，请忽略此问题变得不响应。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>UsbVerifierFailChainedMdlSupport</strong></p>
<p>失败对这些例程的客户端驱动程序的调用时调用方传递中的 GUID_USB_CAPABILITY_CHAINED_MDLS <em>CapabilityType</em>参数。</p>
<ul>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh406230" data-raw-source="[&lt;strong&gt;USBD_QueryUsbCapability&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406230)"><strong>USBD_QueryUsbCapability</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh439434" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceQueryUsbCapability&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439434)"><strong>WdfUsbTargetDeviceQueryUsbCapability</strong></a></li>
</ul></td>
<td><ul>
<li>0:设置处于禁用状态。</li>
<li>1：调用将始终失败。</li>
<li><em>N</em>:调用将失败的概率为 1 /<em>N</em>，其中<em>N</em>是介于 1 到 0x7FF 之间的十六进制值。 例如，如果<em>N</em>为 10。 调用失败一次每个 10 次调用。</li>
</ul></td>
<td><p><strong>与主机控制器不支持的通信链接 MDLs。</strong></p>
<p>为了使客户端驱动程序将发送链接 MDLs (请参阅<a href="https://msdn.microsoft.com/library/windows/hardware/ff565421" data-raw-source="[MDL](https://msdn.microsoft.com/library/windows/hardware/ff565421)">MDL</a>)，USB 驱动程序堆栈和主机控制器必须支持它们。</p>
<p>此设置，以测试客户端驱动程序发送到设备连接到不支持它们的主控制器的链接的 MDL 请求时执行代码。 调用失败而不考虑主机控制器是否支持连锁的 MDLs。</p>
<p>有关 USB 驱动程序堆栈中的链接 MDLs 支持的详细信息，请参阅<a href="how-to-send-chained-mdls.md" data-raw-source="[How to Send Chained MDLs](how-to-send-chained-mdls.md)">如何发送链接 MDLs</a>。</p>
<p>预期的客户端驱动程序行为时主机控制器不支持链接 MDLs:</p>
<ul>
<li><p>该驱动程序应继续执行而无需使用链接的 MDLs I/O 传输。 通过此操作，还将确保您的驱动程序适用于 USB 2.0 主控制器，因为这些控制器不支持链接 MDLs。</p></li>
<li><p>该驱动程序不得导致系统崩溃或通过选择，请忽略此问题变得不响应。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>UsbVerifierFailStaticStreamsSupport</strong></p>
<p>失败对这些例程的客户端驱动程序的调用时调用方传递中的 GUID_USB_CAPABILITY_STATIC_STREAMS <em>CapabilityType</em>参数。</p>
<ul>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh406230" data-raw-source="[&lt;strong&gt;USBD_QueryUsbCapability&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406230)"><strong>USBD_QueryUsbCapability</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh439434" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceQueryUsbCapability&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439434)"><strong>WdfUsbTargetDeviceQueryUsbCapability</strong></a></li>
</ul></td>
<td><ul>
<li>0:设置处于禁用状态。</li>
<li>1：调用将始终失败。</li>
<li><em>N</em>:调用将失败的概率为 1 /<em>N</em>，其中<em>N</em>是介于 1 到 0x7FF 之间的十六进制值。 例如，如果<em>N</em>为 10。 调用将失败一次每个 10 次调用。</li>
</ul></td>
<td><p><strong>与主机控制器不支持静态流的通信。</strong></p>
<p>客户端驱动程序通过静态流的大容量终结点发送的 I/O 传输，主机控制器必须支持流。</p>
<p>如果设备连接到不支持流的主控制器和驱动程序将尝试执行流 I/O 传输，这些传输将会失败。 此设置，若要测试此类在出现故障时的代码。</p>
<p>主控制器不支持静态流时预期的客户端驱动程序行为：</p>
<ul>
<li><p>如果客户端驱动程序想要使用不支持流的 xHCI 控制器，设备必须能够在无需使用启用了流的大容量终结点。</p></li>
<li><p>该驱动程序不得导致系统崩溃或通过选择，请忽略此问题变得不响应。</p></li>
</ul></td>
</tr>
<tr class="even">
<td><p><strong>UsbVerifierStaticStreamCountOverride</strong></p>
更改在获得的值<em>OutputBuffer</em>参数时，客户端调用 GUID_USB_CAPABILITY_STATIC_STREAMS 使用这些例程。
<ul>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh406230" data-raw-source="[&lt;strong&gt;USBD_QueryUsbCapability&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406230)"><strong>USBD_QueryUsbCapability</strong></a></li>
<li><a href="https://msdn.microsoft.com/library/windows/hardware/hh439434" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceQueryUsbCapability&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439434)"><strong>WdfUsbTargetDeviceQueryUsbCapability</strong></a></li>
</ul>
<p><em>OutputBuffer</em>值表示主机控制器支持的静态流的最大数目。</p></td>
<td><ul>
<li>0:设置处于禁用状态。</li>
<li>1：验证程序选择<em>OutputBuffer</em>随机值。 此值可用于压力测试，因为<em>OutputBuffer</em>不重复值，并在调用测试具有多个变体。</li>
<li><p><em>N</em>:指定<em>OutputBuffer</em>值。</p>
<p>当与启用该标志<em>N</em>值， <em>N</em>必须早于 USB 驱动程序堆栈支持的流的最大数目。 因此，然后再设置此标志，必须在检索通过成功调用的实际值。</p>
<p>如果<em>N</em>大于最大数量的流，设置将被忽略。</p></li>
</ul></td>
<td><p><strong>与不同的主机控制器的通信，每个都支持不同的值的流的最大数量。</strong></p>
<p>通过使用此设置，可以确保该驱动程序的流处理逻辑的工作方式，而不考虑流支持的不同主机控制器的数量。</p>
<p>将通过主机控制器支持的流的数量限制可用于 I/O 传输的流的数量。</p>
<p>有关如何在客户端驱动程序中支持静态流的信息，请参阅<a href="how-to-open-streams-in-a-usb-endpoint.md" data-raw-source="[How to Open and Close Static Streams in a USB Bulk Endpoint](how-to-open-streams-in-a-usb-endpoint.md)">如何打开和关闭 USB 大容量终结点中的静态流</a>。</p>
<p>当主机控制器支持终结点比少流时预期的客户端驱动程序行为：</p>
<ul>
<li><p>客户端驱动程序可以选择执行具有较少数量的流的数据传输。</p></li>
<li><p>该驱动程序不得导致系统崩溃或通过选择，请忽略此问题变得不响应。</p></li>
</ul></td>
</tr>
<tr class="odd">
<td><p><strong>UsbVerifierFailEnableStaticStreams</strong></p>
<p>客户端驱动程序的打开的静态流请求 (URB_FUNCTION_OPEN_STATIC_STREAMS) 失败。</p></td>
<td><ul>
<li>0:设置处于禁用状态。</li>
<li>1：请求始终会失败。</li>
<li><em>N</em>:请求失败，出现的概率为 1 /<em>N</em>，其中<em>N</em>是介于 1 到 0x7FF 之间的十六进制值。 例如，如果<em>N</em>为 10。 请求失败一次每个 10 次调用。</li>
</ul>
<div class="alert">
<strong>请注意</strong>打开的静态流请求失败，如果以前调用<a href="https://msdn.microsoft.com/library/windows/hardware/hh406230" data-raw-source="[&lt;strong&gt;USBD_QueryUsbCapability&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh406230)"> <strong>USBD_QueryUsbCapability</strong> </a>或<a href="https://msdn.microsoft.com/library/windows/hardware/hh439434" data-raw-source="[&lt;strong&gt;WdfUsbTargetDeviceQueryUsbCapability&lt;/strong&gt;](https://msdn.microsoft.com/library/windows/hardware/hh439434)"> <strong>WdfUsbTargetDeviceQueryUsbCapability</strong> </a>失败。
</div>
<div>
 
</div></td>
<td><p><strong>由于其他原因而失败与支持静态流，但该请求的主控制器的通信。</strong></p>
<p>例如，你的设备连接到支持流的主控制器。 客户端驱动程序将发送一个打开的流请求数 （若要打开的流） 超过了主机控制器支持的流的最大数目。 USB 驱动程序堆栈将无法满足此类请求。</p>
<p>通过使用此设置，可以测试的错误处理打开的流请求失败的代码。</p>
<p>打开流请求失败时预期的客户端驱动程序行为：</p>
<ul>
<li><p>该驱动程序不应继续照常工作。</p></li>
<li><p>该驱动程序不得导致系统崩溃或通过选择，请忽略此问题变得不响应。</p></li>
</ul></td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[**USBD\_CreateHandle**](https://msdn.microsoft.com/library/windows/hardware/hh406241)  
[**USBD\_QueryUsbCapability**](https://msdn.microsoft.com/library/windows/hardware/hh406230)  
[如何打开和关闭 USB 大容量终结点中的静态流](how-to-open-streams-in-a-usb-endpoint.md)  
[如何发送链接 MDLs](how-to-send-chained-mdls.md)  
[USB 诊断和测试指南](usb-driver-testing-guide.md)  



