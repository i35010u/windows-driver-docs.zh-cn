---
title: 串行 I/O 请求接口
description: 若要控制连接到串行控制器上某个端口的外围设备，客户端应用程序或外围设备驱动程序将 i/o 请求发送到端口。
ms.assetid: D536A0EC-2B8B-491B-8A14-656F4B5A3843
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2e2a8b69749c176b5430df5e309258aff226e41d
ms.sourcegitcommit: e769619bd37e04762c77444e8b4ce9fe86ef09cb
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89188949"
---
# <a name="serial-io-request-interface"></a>串行 I/O 请求接口

若要控制连接到串行控制器上某个端口的外围设备，客户端应用程序或外围设备驱动程序将 i/o 请求发送到端口。 客户端使用 [**IRP \_ mj \_ WRITE**](/previous-versions/ff546904(v=vs.85)) 和 [**irp \_ mj \_ 读取**](/previous-versions/ff546883(v=vs.85)) 请求将数据传输到串行端口并从中接收数据。 此外，Windows 定义了一组串行 i/o 控制请求 (IOCTLs) ，客户端可以使用这些请求来配置串行端口。

串行**IRP \_ MJ \_ <em>XXX</em> **请求和串行 IOCTLs 一起构成了一系列串行控制器设备支持的串行 i/o 请求接口。 此接口受 Serial.sys 驱动程序的支持，以及 SerCx2 或 SerCx 的组合以及基于扩展的串行控制器驱动程序。

SerCx2、SerCx 和 Serial.sys 支持许多相同的串行 IOCTLs。 但是，SerCx2、SerCx 和 Serial.sys 支持 *串行设备控制请求*中指定的 IOCTLs 的不同子集。 下表汇总了 SerCx2、SerCx 和 Serial.sys 支持的 IOCTLs 子集。 表中的 **"是"** 条目指示串行框架扩展或驱动程序支持相应的 IOCTL，而 " **无** " 条目指示它不存在。

<table>
<colgroup>
<col width="25%" />
<col width="25%" />
<col width="25%" />
<col width="25%" />
</colgroup>
<thead>
<tr class="header">
<th>串行 IOCTL</th>
<th>SerCx2</th>
<th>SerCx</th>
<th>Serial.sys</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_apply_default_configuration" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_APPLY_DEFAULT_CONFIGURATION&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_apply_default_configuration)"><strong>IOCTL_SERIAL_APPLY_DEFAULT_CONFIGURATION</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>否</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_clear_stats" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_CLEAR_STATS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_clear_stats)"><strong>IOCTL_SERIAL_CLEAR_STATS</strong></a></p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_clr_dtr" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_CLR_DTR&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_clr_dtr)"><strong>IOCTL_SERIAL_CLR_DTR</strong></a></p></td>
<td><p>见第 1 条注释。</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_clr_rts" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_CLR_RTS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_clr_rts)"><strong>IOCTL_SERIAL_CLR_RTS</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_config_size" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_CONFIG_SIZE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_config_size)"><strong>IOCTL_SERIAL_CONFIG_SIZE</strong></a></p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_baud_rate" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_BAUD_RATE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_baud_rate)"><strong>IOCTL_SERIAL_GET_BAUD_RATE</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_chars" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_CHARS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_chars)"><strong>IOCTL_SERIAL_GET_CHARS</strong></a></p></td>
<td><p>请参阅注释2。</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_commstatus" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_COMMSTATUS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_commstatus)"><strong>IOCTL_SERIAL_GET_COMMSTATUS</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_dtrrts" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_DTRRTS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_dtrrts)"><strong>IOCTL_SERIAL_GET_DTRRTS</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_handflow" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_HANDFLOW&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_handflow)"><strong>IOCTL_SERIAL_GET_HANDFLOW</strong></a></p></td>
<td><p>见第 1 条注释。</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_line_control" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_LINE_CONTROL&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_line_control)"><strong>IOCTL_SERIAL_GET_LINE_CONTROL</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_modem_control" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_MODEM_CONTROL&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_modem_control)"><strong>IOCTL_SERIAL_GET_MODEM_CONTROL</strong></a> (参阅备注 4. ) </p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_modemstatus" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_MODEMSTATUS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_modemstatus)"><strong>IOCTL_SERIAL_GET_MODEMSTATUS</strong></a></p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_properties" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_PROPERTIES&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_properties)"><strong>IOCTL_SERIAL_GET_PROPERTIES</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_stats" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_STATS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_stats)"><strong>IOCTL_SERIAL_GET_STATS</strong></a></p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_timeouts" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_TIMEOUTS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_timeouts)"><strong>IOCTL_SERIAL_GET_TIMEOUTS</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_wait_mask" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_GET_WAIT_MASK&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_get_wait_mask)"><strong>IOCTL_SERIAL_GET_WAIT_MASK</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_immediate_char" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_IMMEDIATE_CHAR&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_immediate_char)"><strong>IOCTL_SERIAL_IMMEDIATE_CHAR</strong></a></p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_lsrmst_insert" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_LSRMST_INSERT&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_lsrmst_insert)"><strong>IOCTL_SERIAL_LSRMST_INSERT</strong></a></p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_purge" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_PURGE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_purge)"><strong>IOCTL_SERIAL_PURGE</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_reset_device" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_RESET_DEVICE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_reset_device)"><strong>IOCTL_SERIAL_RESET_DEVICE</strong></a> (参阅注释 5. ) </p></td>
<td><p>否</p></td>
<td><p>否</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_baud_rate" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_BAUD_RATE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_baud_rate)"><strong>IOCTL_SERIAL_SET_BAUD_RATE</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_break_off" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_BREAK_OFF&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_break_off)"><strong>IOCTL_SERIAL_SET_BREAK_OFF</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_break_on" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_BREAK_ON&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_break_on)"><strong>IOCTL_SERIAL_SET_BREAK_ON</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_chars" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_CHARS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_chars)"><strong>IOCTL_SERIAL_SET_CHARS</strong></a></p></td>
<td><p>请参阅注释2。</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_dtr" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_DTR&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_dtr)"><strong>IOCTL_SERIAL_SET_DTR</strong></a></p></td>
<td><p>见第 1 条注释。</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_fifo_control" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_FIFO_CONTROL&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_fifo_control)"><strong>IOCTL_SERIAL_SET_FIFO_CONTROL</strong></a></p></td>
<td><p>见第 1 条注释。</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_handflow" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_HANDFLOW&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_handflow)"><strong>IOCTL_SERIAL_SET_HANDFLOW</strong></a> (参阅备注 3. ) </p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_line_control" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_LINE_CONTROL&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_line_control)"><strong>IOCTL_SERIAL_SET_LINE_CONTROL</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_modem_control" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_MODEM_CONTROL&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_modem_control)"><strong>IOCTL_SERIAL_SET_MODEM_CONTROL</strong></a> (参阅备注 4. ) </p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_queue_size" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_QUEUE_SIZE&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_queue_size)"><strong>IOCTL_SERIAL_SET_QUEUE_SIZE</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_rts" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_RTS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_rts)"><strong>IOCTL_SERIAL_SET_RTS</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_timeouts" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_TIMEOUTS&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_timeouts)"><strong>IOCTL_SERIAL_SET_TIMEOUTS</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_wait_mask" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_WAIT_MASK&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_wait_mask)"><strong>IOCTL_SERIAL_SET_WAIT_MASK</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_xoff" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_XOFF&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_xoff)"><strong>IOCTL_SERIAL_SET_XOFF</strong></a></p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_xon" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_SET_XON&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_set_xon)"><strong>IOCTL_SERIAL_SET_XON</strong></a></p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_wait_on_mask" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_WAIT_ON_MASK&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_wait_on_mask)"><strong>IOCTL_SERIAL_WAIT_ON_MASK</strong></a></p></td>
<td><p>是</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
<tr class="even">
<td><p><a href="https://docs.microsoft.com/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_xoff_counter" data-raw-source="[&lt;strong&gt;IOCTL_SERIAL_XOFF_COUNTER&lt;/strong&gt;](/windows-hardware/drivers/ddi/ntddser/ni-ntddser-ioctl_serial_xoff_counter)"><strong>IOCTL_SERIAL_XOFF_COUNTER</strong></a></p></td>
<td><p>否</p></td>
<td><p>是</p></td>
<td><p>是</p></td>
</tr>
</tbody>
</table>


**备注**

1. 根据串行控制器驱动程序的实现和串行控制器硬件的功能，SerCx2 可能支持也可能不支持此 IOCTL。

2. SerCx2 不支持特殊字符。 SerCx2 始终完成具有状态 "成功" 状态代码的 **IOCTL \_ 串行 \_ 组 \_ 字符** 请求 \_ ，但不会设置任何特殊字符，也不会执行任何其他操作来响应此请求。 对于 **IOCTL \_ 序列 \_ 获取 \_ 字符** 请求，SerCx2 将 [**串行 \_ 字符**](/windows-hardware/drivers/ddi/ntddser/ns-ntddser-_serial_chars) 结构中的所有字符值设置为 null，并完成状态为 " \_ 成功" 状态代码的请求。

3. SerCx2 和 SerCx 仅支持为**串行 \_ HANDFLOW**结构的**FlowReplace**和**ControlHandShake**成员定义的标志的子集。 Serial.sys 支持所有这些标志。 有关详细信息，请参阅 [**SERIAL \_ HANDFLOW**](/windows-hardware/drivers/ddi/ntddser/ns-ntddser-_serial_handflow)。

4. **Ioctl \_ 串行 \_ 获取 \_ 调制解调器 \_ 控制**和**ioctl \_ 串行 \_ 集 \_ 调制解调器 \_ 控制**请求主要用于硬件测试。 没有为调制解调器控制操作定义标准寄存器布局。 使用调制解调器控制 IOCTLs 的外围设备驱动程序会导致自身依赖于特定串行控制器的硬件功能。

5. Serial.sys 驱动程序始终完成具有状态成功的 **IOCTL \_ 串行 \_ 重置 \_ 设备** 请求 \_ ，但不执行任何操作来响应此请求。 SerCx2 和 SerCx 不支持 **IOCTL \_ 串行 \_ 重置 \_ 设备** 请求，并始终完成这些请求，状态为 " \_ 未实现" \_ 。

有关**IOCTL \_ 串行 \_ <em>XXX</em> **请求以及串行控制器的读取和写入请求的详细信息，请参阅[ntddser](/windows-hardware/drivers/ddi/ntddser/)标头。