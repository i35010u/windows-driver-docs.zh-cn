---
title: 完成 I/O 请求时指定优先级提升
description: 完成 I/O 请求时指定优先级提升
ms.assetid: 9a501ca1-58c9-4458-b202-9581f8ce5e5f
keywords:
- 请求处理 WDK KMDF，优先级提升
- 优先级提升 WDK KMDF
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 9c8098efd572c9be60b320f598e3392a5ab943f1
ms.sourcegitcommit: 4b7a6ac7c68e6ad6f27da5d1dc4deabd5d34b748
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/24/2019
ms.locfileid: "72842191"
---
# <a name="specifying-priority-boosts-when-completing-io-requests"></a>完成 I/O 请求时指定优先级提升


当驱动程序完成 i/o 请求时，它可以调用[**WdfRequestCompleteWithPriorityBoost**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)来指定一个值，系统使用该值来提升请求 i/o 操作的线程的运行时优先级。

如果驱动程序调用[**WdfRequestComplete**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcomplete)或[**WdfRequestCompleteWithInformation**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithinformation)而不是[**WdfRequestCompleteWithPriorityBoost**](https://docs.microsoft.com/windows-hardware/drivers/ddi/wdfrequest/nf-wdfrequest-wdfrequestcompletewithpriorityboost)，则框架将使用基于设备类型的默认优先级提升值。 下表列出了框架使用的默认优先级提升值。 在*Wdm .h*中定义了设备类型和优先级提升常数。

<table>
<colgroup>
<col width="50%" />
<col width="50%" />
</colgroup>
<thead>
<tr class="header">
<th align="left">设备类型</th>
<th align="left">默认优先级提升</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_UNDEFINED</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_BEEP</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_CD_ROM</p></td>
<td align="left"><p>IO_CD_ROM_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_CD_ROM_FILE_SYSTEM</p></td>
<td align="left"><p>IO_CD_ROM_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_CONTROLLER</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_DATALINK</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_DFS</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_DISK</p></td>
<td align="left"><p>IO_DISK_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_DISK_FILE_SYSTEM</p></td>
<td align="left"><p>IO_DISK_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_FILE_SYSTEM</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_INPORT_PORT</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_KEYBOARD</p></td>
<td align="left"><p>IO_KEYBOARD_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_MAILSLOT</p></td>
<td align="left"><p>IO_MAILSLOT_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_MIDI_IN</p></td>
<td align="left"><p>IO_SOUND_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_MIDI_OUT</p></td>
<td align="left"><p>IO_SOUND_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_MOUSE</p></td>
<td align="left"><p>IO_MOUSE_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_MULTI_UNC_PROVIDER</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_NAMED_PIPE</p></td>
<td align="left"><p>IO_NAMED_PIPE_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_NETWORK</p></td>
<td align="left"><p>IO_NETWORK_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_NETWORK_BROWSER</p></td>
<td align="left"><p>IO_NETWORK_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_NETWORK_FILE_SYSTEM</p></td>
<td align="left"><p>IO_NETWORK_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_NULL</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_PARALLEL_PORT</p></td>
<td align="left"><p>IO_PARALLEL_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_PHYSICAL_NETCARD</p></td>
<td align="left"><p>IO_NETWORK_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_PRINTER</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_SCANNER</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_SERIAL_MOUSE_PORT</p></td>
<td align="left"><p>IO_SERIAL_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_SERIAL_PORT</p></td>
<td align="left"><p>IO_SERIAL_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_SCREEN</p></td>
<td align="left"><p>IO_VIDEO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_SOUND</p></td>
<td align="left"><p>IO_SOUND_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_STREAMS</p></td>
<td align="left"><p>IO_SOUND_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_TAPE</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_TAPE_FILE_SYSTEM</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_TRANSPORT</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_UNKNOWN</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_VIDEO</p></td>
<td align="left"><p>IO_VIDEO_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_VIRTUAL_DISK</p></td>
<td align="left"><p>IO_DISK_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_WAVE_IN</p></td>
<td align="left"><p>IO_SOUND_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_WAVE_OUT</p></td>
<td align="left"><p>IO_SOUND_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_8042_PORT</p></td>
<td align="left"><p>IO_KEYBOARD_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_NETWORK_REDIRECTOR</p></td>
<td align="left"><p>IO_NETWORK_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_BATTERY</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_BUS_EXTENDER</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_MODEM</p></td>
<td align="left"><p>IO_SERIAL_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_VDM</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_MASS_STORAGE</p></td>
<td align="left"><p>IO_DISK_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_SMB</p></td>
<td align="left"><p>IO_NETWORK_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_KS</p></td>
<td align="left"><p>IO_SOUND_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_CHANGER</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_SMARTCARD</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_ACPI</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_DVD</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_FULLSCREEN_VIDEO</p></td>
<td align="left"><p>IO_VIDEO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_DFS_FILE_SYSTEM</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_DFS_VOLUME</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_SERENUM</p></td>
<td align="left"><p>IO_SERIAL_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_TERMSRV</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_KSEC</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="odd">
<td align="left"><p>FILE_DEVICE_FIPS</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
<tr class="even">
<td align="left"><p>FILE_DEVICE_INFINIBAND</p></td>
<td align="left"><p>IO_NO_INCREMENT</p></td>
</tr>
</tbody>
</table>

 

 

 





