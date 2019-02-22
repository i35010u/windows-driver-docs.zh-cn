---
title: 处理磁带设备控制请求
description: 处理磁带设备控制请求
ms.assetid: de6edfc6-9b4b-4866-8fdb-1047b43163de
keywords:
- 磁带驱动程序 WDK 存储映射状态的值
- 存储磁带驱动程序 WDK，映射状态的值
- TAPE_STATUS_SEND_SRB_AND_CALLBACK
- TAPE_STATUS_CHECK_TEST_UNIT_READY
- TAPE_STATUS_CALLBACK
- TAPE_STATUS_REQUIRES_CLEANING
- TAPE_STATUS
- 映射 TAPE_STATUS 值
- 状态值 WDK 磁带
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 06195bcdc418417fb497bdbacb6d9313d8af51b2
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56525948"
---
# <a name="processing-tape-device-control-requests"></a>处理磁带设备控制请求


## <span id="ddk_processing_tape_device_control_requests_kg"></span><span id="DDK_PROCESSING_TAPE_DEVICE_CONTROL_REQUESTS_KG"></span>


所有磁带 miniclass 驱动程序必须使用所列的值的状态都报告[**磁带\_状态**](https://msdn.microsoft.com/library/windows/hardware/ff567975)枚举器。 但是，磁带类驱动程序完成的 I/O 控制请求，它将报告使用等效的 NT 状态值的状态。 下表提供了磁带之间的映射\_状态值和其等效的 NT 状态值：

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

 

无论在类驱动程序必须调用 miniclass 例程不止一次以完成请求，miniclass 驱动程序将使用返回的状态以指示请求是否已完成或是否应再次调用该例程。 磁带类驱动程序维护的次数，它为给定的请求并将计算传递给为例程称为 miniclass 例程的从零开始计数*CallNumber*参数。

Miniclass 例程将返回以指示类驱动程序应再次调用该例程的以下状态值之一：

-   磁带\_状态\_发送\_SRB\_AND\_回调

    此返回值指示磁带类驱动程序将 SRB 发送到设备。 填写 SRB 经过磁带类驱动程序后，磁带 miniclass 例程通常返回此状态。 如果操作成功，此类驱动程序递增*CallNumber*并再次调用 miniclass 例程。 如果 SRB 失败，类驱动程序会调用 miniclass 例程，具体取决于值再次*RetryFlags*。

-   磁带\_状态\_检查\_测试\_单元\_准备就绪

    此返回值指示磁带类驱动程序创建测试单元准备命令 SRB，SRB 发送到设备。

-   磁带\_状态\_回调

    此返回值指示磁带类驱动程序来递增*CallNumber*不向设备发送 SRB。 这简化了支持多个设备的 case 语句。 例如，假设大部分特定 miniclass 驱动程序支持的磁带设备，需要三个 Srb 处理特定请求。 一台设备，但是，需要仅第一个和第三个 Srb。 对于唯一的设备磁带 miniclass 驱动程序可以返回磁带\_状态\_回调以跳过第二个 SRB，从而允许驱动程序使用相同的代码来处理它支持的所有设备的请求。

-   磁带\_状态\_REQUIRES\_清理

    如果磁带设备支持清洗通知中检测数据，而不是错误，磁带 miniclass 驱动程序的 TapeMiniGetStatus 例程将返回此状态可指示驱动器需要清洗磁带类驱动程序。

当 miniclass 例程完成请求的处理-成功或有错误后重试次数用完-返回到磁带类驱动程序且其中装有磁带\_状态\_*XXX* ，该值指示成功或失败的请求。

 

 




