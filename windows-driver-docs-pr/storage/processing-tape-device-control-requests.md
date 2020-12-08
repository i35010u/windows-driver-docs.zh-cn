---
title: 处理磁带设备控制请求
description: 处理磁带设备控制请求
keywords:
- 磁带驱动程序 WDK 存储，映射状态值
- 存储磁带驱动程序 WDK，映射状态值
- TAPE_STATUS_SEND_SRB_AND_CALLBACK
- TAPE_STATUS_CHECK_TEST_UNIT_READY
- TAPE_STATUS_CALLBACK
- TAPE_STATUS_REQUIRES_CLEANING
- TAPE_STATUS
- 映射 TAPE_STATUS 值
- status 值 WDK 磁带
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0895da0c6b2e98c692953ecdd8eb312b5ed2ee44
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830955"
---
# <a name="processing-tape-device-control-requests"></a>处理磁带设备控制请求


## <span id="ddk_processing_tape_device_control_requests_kg"></span><span id="DDK_PROCESSING_TAPE_DEVICE_CONTROL_REQUESTS_KG"></span>


所有磁带 miniclass 驱动程序必须使用 [**磁带 \_ 状态**](/windows-hardware/drivers/ddi/minitape/ne-minitape-_tape_status) 枚举器中列出的值报告状态。 但是，当磁带类驱动程序完成 i/o 控制请求时，它将使用等效的 NT 状态值报告状态。 下表提供了磁带 \_ 状态值和其等效的 NT 状态值之间的映射：

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">NT 状态值</th>
<th align="left">磁带状态值</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>STATUS_INSUFFICIENT_RESOURCES</p></td>
<td align="left"><p>TAPE_STATUS_INSUFFICIENT_RESOURCES</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_NOT_IMPLEMENTED</p></td>
<td align="left"><p>TAPE_STATUS_NOT_IMPLEMENTED</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_INVALID_DEVICE_REQUEST</p></td>
<td align="left"><p>TAPE_STATUS_INVALID_DEVICE_REQUEST</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_INVALID_PARAMETER</p></td>
<td align="left"><p>TAPE_STATUS_INVALID_PARAMETER</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_VERIFY_REQUIRED</p></td>
<td align="left"><p>TAPE_STATUS_MEDIA_CHANGED</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_BUS_RESET</p></td>
<td align="left"><p>TAPE_STATUS_BUS_RESET</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_SETMARK_DETECTED</p></td>
<td align="left"><p>TAPE_STATUS_SETMARK_DETECTED</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_FILEMARK_DETECTED</p></td>
<td align="left"><p>TAPE_STATUS_FILEMARK_DETECTED</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_BEGINNING_OF_MEDIA</p></td>
<td align="left"><p>TAPE_STATUS_BEGINNING_OF_MEDIA</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_END_OF_MEDIA</p></td>
<td align="left"><p>TAPE_STATUS_END_OF_MEDIA</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_BUFFER_OVERFLOW</p></td>
<td align="left"><p>TAPE_STATUS_BUFFER_OVERFLOW</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_NO_DATA_DETECTED</p></td>
<td align="left"><p>TAPE_STATUS_NO_DATA_DETECTED</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_EOM_OVERFLOW</p></td>
<td align="left"><p>TAPE_STATUS_EOM_OVERFLOW</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_NO_MEDIA</p></td>
<td align="left"><p>TAPE_STATUS_NO_MEDIA</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_IO_DEVICE_ERROR</p></td>
<td align="left"><p>TAPE_STATUS_IO_DEVICE_ERROR</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_UNRECOGNIZED_MEDIA</p></td>
<td align="left"><p>TAPE_STATUS_UNRECOGNIZED_MEDIA</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_DEVICE_NOT_READY</p></td>
<td align="left"><p>TAPE_STATUS_DEVICE_NOT_READY</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_MEDIA_WRITE_PROTECTED</p></td>
<td align="left"><p>TAPE_STATUS_MEDIA_WRITE_PROTECTED</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_DEVICE_DATA_ERROR</p></td>
<td align="left"><p>TAPE_STATUS_DEVICE_DATA_ERROR</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_NO_SUCH_DEVICE</p></td>
<td align="left"><p>TAPE_STATUS_NO_SUCH_DEVICE</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_INVALID_BLOCK_LENGTH</p></td>
<td align="left"><p>TAPE_STATUS_INVALID_BLOCK_LENGTH</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_IO_TIMEOUT</p></td>
<td align="left"><p>TAPE_STATUS_IO_TIMEOUT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_DEVICE_NOT_CONNECTED</p></td>
<td align="left"><p>TAPE_STATUS_DEVICE_NOT_CONNECTED</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_DATA_OVERRUN</p></td>
<td align="left"><p>TAPE_STATUS_DATA_OVERRUN</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_DEVICE_BUSY</p></td>
<td align="left"><p>TAPE_STATUS_DEVICE_BUSY</p></td>
</tr>
<tr class="even">
<td align="left"><p>STATUS_DEVICE_REQUIRES_CLEANING</p></td>
<td align="left"><p>TAPE_STATUS_REQUIRES_CLEANING</p></td>
</tr>
<tr class="odd">
<td align="left"><p>STATUS_CLEANER_CARTRIDGE_INSTALLED</p></td>
<td align="left"><p>TAPE_STATUS_CLEANER_CARTRIDGE_INSTALLED</p></td>
</tr>
</tbody>
</table>

 

每当类驱动程序必须多次调用 miniclass 例程才能完成请求时，miniclass 驱动程序将使用返回状态来指示请求是否已完成，或是否应再次调用例程。 磁带类驱动程序维护给定请求的 miniclass 例程的从零开始的计数，并将该计数作为 *CallNumber* 参数传递到例程。

Miniclass 例程返回以下状态值之一，指示类驱动程序应再次调用例程：

-   磁带 \_ 状态 \_ 发送 \_ SRB \_ 和 \_ 回拨

    此返回值指示磁带类驱动程序将 SRB 发送到设备。 磁带 miniclass 例程在填充由磁带类驱动程序传递的 SRB 后，通常会返回此状态。 如果操作成功，类驱动程序将递增 *CallNumber* 并再次调用 miniclass 例程。 如果 SRB 失败，类驱动程序将再次调用 miniclass 例程，具体取决于 *RetryFlags* 的值。

-   磁带 \_ 状态 \_ 检查 \_ 测试 \_ 单元 \_ 就绪

    此返回值指示磁带类驱动程序为 "测试单元准备" 命令创建 SRB，并将 SRB 发送到设备。

-   磁带 \_ 状态 \_ 回拨

    此返回值指示磁带类驱动程序递增 *CallNumber* ，而无需将 SRB 发送到设备。 这会简化支持多个设备的 case 语句。 例如，假定特定 miniclass 驱动程序支持的大多数磁带设备需要三个 SRBs 来处理某个请求。 不过，一个设备只需要第一个和第三个 SRBs。 对于唯一设备，磁带 miniclass 驱动程序可以返回磁带 \_ 状态 \_ 回拨，以跳过第二个 SRB，使驱动程序可以使用相同的代码来处理该请求所支持的所有设备。

-   磁带 \_ 状态 \_ 需要 \_ 清除

    如果磁带设备支持在感知数据中清除通知而不是错误，则磁带 miniclass 驱动程序的 TapeMiniGetStatus 例程将返回此状态，以指示磁带机需要清洗的磁带类驱动程序。

当 miniclass 例程完成处理请求时，无论是成功完成还是在重试后发生错误，都将返回到磁带类驱动程序，其中包含磁带 \_ 状态 \_ *XXX* ，指示请求是成功还是失败。

 

