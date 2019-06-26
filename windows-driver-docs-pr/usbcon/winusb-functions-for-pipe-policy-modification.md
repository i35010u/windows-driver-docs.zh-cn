---
Description: Winusb.dll 公开 WinUsb_GetPipePolicy 函数以检索管道的默认策略。
title: 用于管道策略修改的 WinUSB 函数
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: ab94d3398371d57831b4f4f4defad7534e92fffe
ms.sourcegitcommit: fb7d95c7a5d47860918cd3602efdd33b69dcf2da
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2019
ms.locfileid: "67385678"
---
# <a name="winusb-functions-for-pipe-policy-modification"></a>用于管道策略修改的 WinUSB 函数


若要启用应用程序来获取和设置管道的默认策略参数的终结点，Winusb.dll 公开[ **WinUsb\_GetPipePolicy** ](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getpipepolicy)函数以检索管道的默认策略。 [ **WinUsb\_SetPipePolicy** ](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_setpipepolicy)函数允许应用程序策略参数设置为新值。

WinUSB，可通过将策略应用到终结点的管道来修改其默认行为。 通过使用这些策略，可以配置 WinUSB 以最能满足您的设备与它的功能。 下表提供了一组受 WinUSB 管道策略。

**请注意**  表所述的策略是仅对指定的终结点有效。 将策略设置其他终结点上具有读取或写入请求 WinUSB 的行为没有影响。

 

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
<th>策略数</th>
<th>策略名称</th>
<th>描述</th>
<th>终结点 （方向）</th>
<th>默认值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>0x01</td>
<td>SHORT_PACKET_TERMINATE</td>
<td>发送缓冲区在其中作为终结点支持的最大数据包大小的倍数的写入请求一个零长度包。</td>
<td><p>大容量 (OUT)</p>
<p>中断 (OUT)</p></td>
<td>FALSE</td>
</tr>
<tr class="even">
<td>0x02</td>
<td>AUTO_CLEAR_STALL</td>
<td>而无需停止数据流，会自动清除已停止的管道。</td>
<td><p>大容量 (IN)</p>
<p>中断 (IN)</p></td>
<td>FALSE</td>
</tr>
<tr class="odd">
<td>0x03</td>
<td>PIPE_TRANSFER_TIMEOUT</td>
<td>取消请求之前等待的超时间隔，以毫秒为单位。</td>
<td><p>大容量 (IN)</p>
<p>大容量 (OUT)</p>
<p>中断 (IN)</p>
<p>中断 (OUT)</p></td>
<td>控件，则为 5 秒 （5000 毫秒）0 表示其他人</td>
</tr>
<tr class="even">
<td>0x04</td>
<td>IGNORE_SHORT_PACKETS</td>
<td>完成的读取的请求时收到短数据包或读取某些字节数。 如果文件大小未知，则会在短数据包上终止请求。</td>
<td><p>大容量 (IN)</p>
<p>中断 (IN)</p></td>
<td>FALSE</td>
</tr>
<tr class="odd">
<td>0x05</td>
<td>ALLOW_PARTIAL_READS</td>
<td>允许读取的请求返回更多的数据不是由调用方请求的设备。</td>
<td><p>大容量 (IN)</p>
<p>中断 (IN)</p></td>
<td>TRUE</td>
</tr>
<tr class="even">
<td>0x06</td>
<td>AUTO_FLUSH</td>
<td>保存中读取请求的过多数据并将其添加到下一步读取请求或放弃过多的数据。</td>
<td><p>大容量 (IN)</p>
<p>中断 (IN)</p></td>
<td>FALSE</td>
</tr>
<tr class="odd">
<td>0x07</td>
<td>RAW_IO</td>
<td>免验证队列和错误处理来提高性能的多个读取请求。</td>
<td><p>大容量 (IN)</p>
<p>中断 (IN)</p></td>
<td>FALSE</td>
</tr>
<tr class="even">
<td>0x08</td>
<td>MAXIMUM_TRANSFER_SIZE</td>
<td>获取受 WinUSB USB 传输的最大大小。 这是一个只读的策略，可以通过调用来检索<a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getpipepolicy" data-raw-source="[&lt;strong&gt;WinUsb_GetPipePolicy&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getpipepolicy)"> <strong>WinUsb_GetPipePolicy</strong></a>。</td>
<td><p>大容量 (IN)</p>
<p>大容量 (OUT)</p>
<p>中断 (IN)</p>
<p>中断 (OUT)</p></td>
<td></td>
</tr>
<tr class="odd">
<td>0x09</td>
<td>RESET_PIPE_ON_RESUME</td>
<td>重置之前接受新请求挂起中恢复之后的终结点的管道。</td>
<td><p>大容量 (IN)</p>
<p>大容量 (OUT)</p>
<p>中断 (IN)</p>
<p>中断 (OUT)</p></td>
<td>FALSE</td>
</tr>
</tbody>
</table>

 

下表标识如何使用每个管道策略的最佳实践，并介绍所产生的行为时启用该策略。

<table>
<colgroup>
<col width="33%" />
<col width="33%" />
<col width="33%" />
</colgroup>
<thead>
<tr class="header">
<th>策略</th>
<th>如果，启用...</th>
<th>行为</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>SHORT_PACKET_TERMINATE(0x01)</td>
<td>设备要求扩展传输以结尾的长度为零的数据包。 大多数设备不具有此要求。</td>
<td><p>如果已启用 (策略参数值是<strong>，则返回 TRUE</strong>或非零值)，每个终结点，支持的最大数据包大小的倍数的写入请求后跟长度为零的数据包。</p>
<p>之后将数据发送到主控制器，WinUSB 发送包含长度为零的数据包的写入请求，然后完成创建请求<a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe" data-raw-source="[&lt;strong&gt;WinUsb_WritePipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_writepipe)"> <strong>WinUsb_WritePipe</strong></a>。</p></td>
</tr>
<tr class="even">
<td>AUTO_CLEAR_STALL</td>
<td>您不希望要使终结点处于已停止状态的失败的传输。 仅当 RAW_IO 处于禁用状态时具有多个挂起的读取的请求到的终结点时，此策略是非常有用。</td>
<td><ul>
<li><p>如果已启用 (策略参数值是<strong>，则返回 TRUE</strong>或非零值)，自动清除停滞条件。 此策略参数不会影响控制管道。</p>
<p>时失败，并且主机控制器返回的状态不是 STATUS_CANCELLED 或 STATUS_DEVICE_NOT_CONNECTED 的读取请求，WinUSB 将完成失败的请求之前重置管道。 重置管道而不会中断流的数据清除的停止条件。 数据将继续，只要新传输保持到达从设备中的终结点的流。 新的传输可以包括一个停止发生时已在队列中。</p>
<p>如果启用此策略不会显著影响性能。</p></li>
<li>如果禁用 (策略参数值是<strong>FALSE</strong>或零)，到达终结点后停止传输的所有传输都失败，直到调用方手动重置终结点的管道，通过调用<a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_resetpipe" data-raw-source="[&lt;strong&gt;WinUsb_ResetPipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_resetpipe)"> <strong>WinUsb_ResetPipe</strong></a>。</li>
</ul></td>
</tr>
<tr class="odd">
<td>PIPE_TRANSFER_TIMEOUT</td>
<td>预计到的终结点的传输将在特定时间内完成。</td>
<td><ul>
<li>如果设置为零 （默认值） 时，传输将不会因为主控制器不将取消传输。 在这种情况下，传输等到无限期地被手动取消或传输正常完成。</li>
<li><p>如果设置为非零值 （超时间隔），主机控制器将启动一个计时器时收到传输请求。 当计时器超过设置的超时间隔时，则会取消该请求。</p>
<p>由于计时器管理会对很小的性能产生负面影响。</p>
<div class="alert">
<strong>请注意</strong>  请求就不会超时 WinUSB 队列中等待时。
<p>在 Windows Vista 中，对 （除 RAW_IO 启用与传输），所有传输 WinUSB 对请求进行排队直到目标终结点上的所有以前的转移已完成。 主控制器不包括在计算中使用的超时间隔的排队时间。</p>
<p>使用启用 RAW_IO，WinUSB 不会排队请求。 相反，它请求将直接传递到 USB 堆栈是否 USB 堆栈正忙于处理以前的转移。 如果 USB 堆栈正忙，它可能会延迟处理新请求。 请注意，这会导致超时。</p>
</div>
<div>
 
</div></li>
</ul></td>
</tr>
<tr class="even">
<td>IGNORE_SHORT_PACKETS</td>
<td>禁用 RAW_IO 并不希望短数据包，以完成读取的请求。</td>
<td><ul>
<li>如果已启用 (策略参数值是<strong>，则返回 TRUE</strong>或非零值)，主机控制器将立即收到短数据包后无法完成读取的操作。 相反，它完成操作仅当：
<ul>
<li>出现错误。</li>
<li>取消该请求。</li>
<li>已接收的所有请求的字节。</li>
</ul></li>
<li>如果禁用 (策略参数值是<strong>FALSE</strong>或零)，主机控制器完成读取的操作后对其具有读取请求的字节数或已接收到一个简短的数据包。</li>
</ul></td>
</tr>
<tr class="odd">
<td>ALLOW_PARTIAL_READS</td>
<td>设备可以发送更多的数据请求。 这是当请求缓冲区的大小是最大的终结点的数据包大小的倍数。
<p>如果你的应用程序想要读取几个字节来确定要读取的总字节数，请使用此选项。</p></td>
<td><ul>
<li>如果禁用 (策略参数值是<strong>FALSE</strong>或零) 和设备返回更多的数据少于请求、 WinUSB 完成并出现错误的请求。</li>
<li><p>如果已启用 (策略参数值是<strong>，则返回 TRUE</strong>或非零) 和设备返回更多的数据少于请求，WinUSB 可以 （具体取决于 AUTO_FLUSH 设置） 添加过多的数据，读请求到下一次读取的开头请求或放弃过多的数据。</p>
<p>如果启用，WinUSB 将立即成功完成读取的请求针对零字节，而不会将堆栈的下层的请求。</p></li>
</ul></td>
</tr>
<tr class="even">
<td>AUTO_FLUSH</td>
<td>启用 ALLOW_PARTIAL _READS 策略。
<p>设备可以发送更多的数据少于请求，并在应用程序不需要任何额外数据。 这是当请求缓冲区的大小是最大的终结点的数据包大小的倍数。</p></td>
<td><p>AUTO_FLUSH 定义时启用 ALLOW_PARTIAL_READS WinUSB 的行为。 如果 ALLOW_PARTIAL_READS 处于禁用状态，被忽略 WinUSB AUTO_FLUSH 值。</p>
<p>WinUSB 可以丢弃剩余数据，或将其发送与调用方的下一步读取请求。</p>
<ul>
<li>如果已启用 (策略参数值是<strong>，则返回 TRUE</strong>或非零值)，WinUSB 丢弃而无需任何错误代码的额外字节。</li>
<li>如果禁用 (策略参数值是<strong>FALSE</strong>或零)，WinUSB 将保存的额外字节、 将它们添加到调用方的下一个读取请求的开始，然后将数据发送到调用方在下一个读取操作。</li>
</ul></td>
</tr>
<tr class="odd">
<td>RAW_IO</td>
<td>性能是优先考虑和应用程序提交到同一个终结点的同时读取的请求。
<p>RAW_IO 施加某些限制由调用方中传递的缓冲区<a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe" data-raw-source="[&lt;strong&gt;WinUsb_ReadPipe&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_readpipe)"> <strong>WinUsb_ReadPipe</strong></a>:</p>
<ul>
<li>缓冲区长度必须最大的终结点的数据包大小的倍数。</li>
<li>长度必须小于或等于的值来检索 MAXIMUM_TRANSFER_SIZE <a href="https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getpipepolicy" data-raw-source="[&lt;strong&gt;WinUsb_GetPipePolicy&lt;/strong&gt;](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getpipepolicy)"> <strong>WinUsb_GetPipePolicy</strong></a>。</li>
</ul></td>
<td><p>如果启用，传输绕过队列和错误处理来提高性能的多个读取请求。 WinUSB 句柄读取请求，如下所示：</p>
<ul>
<li>不是最大的终结点的数据包大小的倍数请求会失败。</li>
<li>大于 WinUSB 支持的最大传输大小的请求会失败。</li>
<li>所有格式正确的请求会立即发送到 USB core 堆栈来计划在主控制器中。</li>
</ul>
启用此设置会大大提高了多个读取请求通过减少一次传输的最后一个数据包和下一步传输的第一个数据包之间的延迟。</td>
</tr>
<tr class="even">
<td>RESET_PIPE_ON_RESUME</td>
<td>设备不会保留其数据切换状态的挂起。</td>
<td>在从挂起中恢复 WinUSB 重置终结点，然后才允许调用方以将新请求发送到终结点。</td>
</tr>
</tbody>
</table>

 

## <a name="related-topics"></a>相关主题
[WinUSB 电源管理](winusb-power-management.md)  
[WinUSB 体系结构和模块](winusb-architecture.md)  
[选择用于开发 USB 客户端驱动程序的驱动程序模型](winusb-considerations.md)  
[WinUSB (Winusb.sys) 安装](winusb-installation.md)  
[如何通过使用 WinUSB 函数访问 USB 设备](using-winusb-api-to-communicate-with-a-usb-device.md)  
[WinUSB 函数](https://docs.microsoft.com/previous-versions/windows/hardware/drivers/ff540046(v=vs.85)#winusb)  
[**WinUsb\_GetPipePolicy**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_getpipepolicy)  
[**WinUsb\_SetPipePolicy**](https://docs.microsoft.com/windows/desktop/api/winusb/nf-winusb-winusb_setpipepolicy)  
[WinUSB](winusb.md)  



