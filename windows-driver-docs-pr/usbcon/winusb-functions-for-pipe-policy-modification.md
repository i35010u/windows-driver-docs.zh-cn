---
description: Winusb.dll 公开 WinUsb_GetPipePolicy 函数以检索管道的默认策略。
title: 用于管道策略修改的 WinUSB 函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 1c81b78194ae4e979e3b3c8d2b578ab67d8de213
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88969350"
---
# <a name="winusb-functions-for-pipe-policy-modification"></a>用于管道策略修改的 WinUSB 函数


若要使应用程序能够获取和设置终结点管道的默认策略参数，Winusb.dll 公开 [**WinUsb \_ GetPipePolicy**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getpipepolicy) 函数以检索管道的默认策略。 [**WinUsb \_ SetPipePolicy**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_setpipepolicy)函数允许应用程序将策略参数设置为新值。

WinUSB 允许您通过将策略应用于终结点的管道来修改其默认行为。 通过使用这些策略，你可以将 WinUSB 配置为将设备最匹配到其功能。 下表提供了 WinUSB 支持的管道策略的列表。

**注意**   表中所述的策略仅对指定的终结点有效。 在其他终结点上设置策略对 WinUSB 对读取或写入请求的行为没有影响。

 

<table>
<colgroup>
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
<col width="20%" />
</colgroup>
<thead>
<tr class="header">
<th>策略编号</th>
<th>策略名称</th>
<th>说明</th>
<th>端点 (方向) </th>
<th>默认值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>0x01</td>
<td>SHORT_PACKET_TERMINATE</td>
<td>发送一个长度为零的数据包，该写入请求中的缓冲区是终结点支持的最大数据包大小的倍数。</td>
<td><p>大容量 () </p>
<p>中断 () </p></td>
<td>FALSE</td>
</tr>
<tr class="even">
<td>0x02</td>
<td>AUTO_CLEAR_STALL</td>
<td>自动清除已停止的管道，而不停止数据流。</td>
<td><p>大容量 () </p>
<p>中断 () </p></td>
<td>FALSE</td>
</tr>
<tr class="odd">
<td>0x03</td>
<td>PIPE_TRANSFER_TIMEOUT</td>
<td>等待超时间隔（以毫秒为单位），然后取消请求。</td>
<td><p>大容量 () </p>
<p>大容量 () </p>
<p>中断 () </p>
<p>中断 () </p></td>
<td>对于 control，为5秒 (5000 毫秒) ;对于其他用户为0</td>
</tr>
<tr class="even">
<td>0x04</td>
<td>IGNORE_SHORT_PACKETS</td>
<td>当收到短数据包或读取特定字节数时，完成读取请求。 如果文件大小未知，请求将在短数据包上终止。</td>
<td><p>大容量 () </p>
<p>中断 () </p></td>
<td>FALSE</td>
</tr>
<tr class="odd">
<td>0x05</td>
<td>ALLOW_PARTIAL_READS</td>
<td>允许来自返回比调用方请求的数据更多的设备的读取请求。</td>
<td><p>大容量 () </p>
<p>中断 () </p></td>
<td>TRUE</td>
</tr>
<tr class="even">
<td>0x06</td>
<td>AUTO_FLUSH</td>
<td>保存读取请求中多余的数据，并将其添加到下一个读取请求或丢弃多余的数据。</td>
<td><p>大容量 () </p>
<p>中断 () </p></td>
<td>FALSE</td>
</tr>
<tr class="odd">
<td>0x07</td>
<td>RAW_IO</td>
<td>绕过排队和错误处理，提高多个读取请求的性能。</td>
<td><p>大容量 () </p>
<p>中断 () </p></td>
<td>FALSE</td>
</tr>
<tr class="even">
<td>0x08</td>
<td>MAXIMUM_TRANSFER_SIZE</td>
<td>获取 WinUSB 支持的 USB 传输的最大大小。 这是一个只读策略，可以通过调用 <a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getpipepolicy" data-raw-source="[&lt;strong&gt;WinUsb_GetPipePolicy&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getpipepolicy)"><strong>WinUsb_GetPipePolicy</strong></a>来检索。</td>
<td><p>大容量 () </p>
<p>大容量 () </p>
<p>中断 () </p>
<p>中断 () </p></td>
<td></td>
</tr>
<tr class="odd">
<td>0x09</td>
<td>RESET_PIPE_ON_RESUME</td>
<td>在接受新请求之前，重置终结点的管道。</td>
<td><p>大容量 () </p>
<p>大容量 () </p>
<p>中断 () </p>
<p>中断 () </p></td>
<td>FALSE</td>
</tr>
</tbody>
</table>

 

下表列出了有关如何使用每个管道策略的最佳实践，以及如何在启用策略时描述产生的行为。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>策略</th>
<th>启用 if .。。</th>
<th>行为</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>SHORT_PACKET_TERMINATE (0x01) </td>
<td>设备要求使用长度为零的数据包终止传输。 大多数设备没有这一要求。</td>
<td><p>如果已启用 (策略参数值为 <strong>TRUE</strong> 或非零) ，则每个写入请求是终结点支持的最大数据包大小的倍数，后面是长度为零的数据包。</p>
<p>将数据发送到主机控制器后，WinUSB 会发送一个包含零长度数据包的写入请求，然后完成 <a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe" data-raw-source="[&lt;strong&gt;WinUsb_WritePipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe)"><strong>WinUsb_WritePipe</strong></a>创建的请求。</p></td>
</tr>
<tr class="even">
<td>AUTO_CLEAR_STALL</td>
<td>不希望失败的传输使终结点处于 "已停止" 状态。 此策略仅在禁用 RAW_IO 时对终结点进行了多个挂起的读取请求时才有用。</td>
<td><ul>
<li><p>如果启用 (策略参数值为 <strong>TRUE</strong> 或非零) ，将自动清除隔栏条件。 此策略参数不影响控制管道。</p>
<p>当读取请求失败并且宿主控制器返回 STATUS_CANCELLED 或 STATUS_DEVICE_NOT_CONNECTED 以外的状态时，WinUSB 将在完成失败请求之前重置管道。 重置管道将清除延迟条件，而不会中断数据流。 只要新的传输一直到达设备，数据就会继续流过终结点。 新传输可以在发生延迟时包含队列中的一个传输。</p>
<p>启用此策略不会对性能产生显著影响。</p></li>
<li>如果已禁用 (策略参数值为 <strong>FALSE</strong> 或零) ，则在停止传输后到达终结点的所有传输都将失败，直到调用方手动重置终结点的 <a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_resetpipe" data-raw-source="[&lt;strong&gt;WinUsb_ResetPipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_resetpipe)"><strong>WinUsb_ResetPipe</strong></a>管道。</li>
</ul></td>
</tr>
<tr class="odd">
<td>PIPE_TRANSFER_TIMEOUT</td>
<td>需要在特定的时间内传输到终结点才能完成。</td>
<td><ul>
<li>如果设置为零 (默认值) ，则传输不会超时，因为主机控制器不会取消传输。 在这种情况下，传输会无限期等待，直到手动取消或传输正常完成。</li>
<li><p>如果设置为非零值 (超时间隔) ，则在接收传输请求时，主机控制器会启动计时器。 当计时器超出设置的超时间隔时，请求将被取消。</p>
<p>由于计时器管理，导致性能下降。</p>
<div class="alert">
<strong>注意</strong>   在 WinUSB 队列中等待时，请求不会超时。
<p>在 Windows Vista 中，对于所有传输 (除了启用了 RAW_IO) 的传输以外，WinUSB 会将请求排队，直到目标终结点上的所有先前传输均已完成。 主机控制器不包括超时间隔计算中的排队时间。</p>
<p>启用 RAW_IO 时，WinUSB 不会对请求进行排队。 相反，它会将请求直接传递到 USB stack，无论 USB 堆栈是否忙于处理以前的传输。 如果 USB stack 处于繁忙状态，它可能会延迟处理新请求。 请注意，这可能会导致超时。</p>
</div>
<div>
 
</div></li>
</ul></td>
</tr>
<tr class="even">
<td>IGNORE_SHORT_PACKETS</td>
<td>RAW_IO 处于禁用状态，并且你不希望短数据包来完成读取请求。</td>
<td><ul>
<li>如果启用 (策略参数值为 <strong>TRUE</strong> 或非零) ，则主机控制器在收到短数据包后将不会立即完成读取操作。 相反，它仅在以下情况下才能完成操作：
<ul>
<li>发生错误。</li>
<li>请求已取消。</li>
<li>已收到所有请求的字节。</li>
</ul></li>
<li>如果已禁用 (策略参数值为 <strong>FALSE</strong> 或零) ，则在读取请求的字节数或接收到短数据包后，主机控制器完成读取操作。</li>
</ul></td>
</tr>
<tr class="odd">
<td>ALLOW_PARTIAL_READS</td>
<td>设备可以发送比请求的更多的数据。 如果请求缓冲区的大小是最大终结点数据包大小的倍数，则可能发生这种情况。
<p>如果你的应用程序想要读取几个字节来确定要读取的总字节数，请使用。</p></td>
<td><ul>
<li>如果已禁用 (策略参数值为 <strong>FALSE</strong> 或零) 并且设备返回比请求的数据多的数据，WinUSB 完成请求并返回错误。</li>
<li><p>如果已启用 (策略参数值为 <strong>TRUE</strong> 或非零) 并且设备返回的数据多于请求的数据，则 WinUSB 可以 (，具体取决于 AUTO_FLUSH 设置) 将多余的数据从读取请求添加到下一个读取请求的开头，或者丢弃多余的数据。</p>
<p>如果启用，WinUSB 会立即成功完成0字节的读取请求，并且不会向堆栈发送请求。</p></li>
</ul></td>
</tr>
<tr class="even">
<td>AUTO_FLUSH</td>
<td>ALLOW_PARTIAL 启用 _READS 策略。
<p>设备可以发送比请求的更多数据，并且你的应用程序不需要任何其他数据。 如果请求缓冲区的大小是最大终结点数据包大小的倍数，则可能发生这种情况。</p></td>
<td><p>AUTO_FLUSH 在启用 ALLOW_PARTIAL_READS 时定义 WinUSB 的行为。 如果禁用 ALLOW_PARTIAL_READS，则 WinUSB 将忽略 AUTO_FLUSH 值。</p>
<p>WinUSB 可以丢弃剩余数据，或将其与调用方的下一个读取请求一起发送。</p>
<ul>
<li>如果启用 (策略参数值为 <strong>TRUE</strong> 或非零) ，则 WinUSB 会丢弃额外的字节，而不会出现任何错误代码。</li>
<li>如果已禁用 (策略参数值为 <strong>FALSE</strong> 或零) ，WinUSB 将保存额外的字节，并将它们添加到调用方的下一个读取请求的开头，然后在下一次读取操作时将数据发送到调用方。</li>
</ul></td>
</tr>
<tr class="odd">
<td>RAW_IO</td>
<td>性能是优先考虑的，应用程序将对同一终结点同时提交读取请求。
<p>RAW_IO 在 <a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe" data-raw-source="[&lt;strong&gt;WinUsb_ReadPipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe)"><strong>WinUsb_ReadPipe</strong></a>中对调用方传递的缓冲区施加某些限制：</p>
<ul>
<li>缓冲区长度必须是最大终结点数据包大小的倍数。</li>
<li>长度必须小于或等于 <a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getpipepolicy" data-raw-source="[&lt;strong&gt;WinUsb_GetPipePolicy&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getpipepolicy)"><strong>WinUsb_GetPipePolicy</strong></a>检索 MAXIMUM_TRANSFER_SIZE 的值。</li>
</ul></td>
<td><p>如果启用，则传输绕过队列和错误处理，以提升多个读取请求的性能。 WinUSB 按如下所示处理读取请求：</p>
<ul>
<li>不是最大终结点数据包大小的倍数的请求失败。</li>
<li>大于 WinUSB 支持的最大传输大小的请求失败。</li>
<li>所有格式正确的请求会立即发送到要在主机控制器中计划的 USB 核心堆栈。</li>
</ul>
如果启用此设置，则可以减少一次传输的最后一个数据包与下一次传输数据包之间的延迟，从而大幅提高多个读取请求的性能。</td>
</tr>
<tr class="even">
<td>RESET_PIPE_ON_RESUME</td>
<td>设备在挂起时不会保持其数据切换状态。</td>
<td>从挂起恢复时，WinUSB 将重置终结点，然后允许调用方将新请求发送到终结点。</td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[WinUSB 电源管理](winusb-power-management.md)  
[WinUSB 体系结构和模块](winusb-architecture.md)  
[选择用于开发 USB 客户端驱动程序的驱动程序模型](winusb-considerations.md)  
[WinUSB (Winusb.sys) 安装](winusb-installation.md)  
[如何通过 WinUSB 函数访问 USB 设备](using-winusb-api-to-communicate-with-a-usb-device.md)  
[WinUSB 函数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)  
[**WinUsb \_ GetPipePolicy**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getpipepolicy)  
[**WinUsb \_ SetPipePolicy**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_setpipepolicy)  
[WinUSB](winusb.md)  



