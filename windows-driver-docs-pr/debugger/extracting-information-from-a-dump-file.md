---
title: 从转储文件中提取信息
description: 从转储文件中提取信息
keywords:
- 提取转储文件中的信息
- 转储文件，提取各种信息
- '用于从转储文件确定的计算机名称 () '
- " (从转储文件确定的计算机名称) "
- '从转储文件 (确定的 IP 地址) '
ms.date: 03/13/2019
ms.localizationpriority: medium
ms.openlocfilehash: 82615887778af6ab01d007d908ff8ca4a37a9438
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96819195"
---
# <a name="extracting-information-from-a-dump-file"></a>从转储文件中提取信息


## <span id="ddk_extracting_information_from_a_dump_file_dbg"></span><span id="DDK_EXTRACTING_INFORMATION_FROM_A_DUMP_FILE_DBG"></span>


某些类型的信息（例如目标计算机的名称）可在实时调试过程中轻松使用。 调试转储文件时，需要执行一些其他操作来确定此信息。

### <a name="span-idfinding_the_computer_name_in_a_kernel_mode_dump_filespanspan-idfinding_the_computer_name_in_a_kernel_mode_dump_filespanfinding-the-computer-name-in-a-kernel-mode-dump-file"></a><span id="finding_the_computer_name_in_a_kernel_mode_dump_file"></span><span id="FINDING_THE_COMPUTER_NAME_IN_A_KERNEL_MODE_DUMP_FILE"></span>在 Kernel-Mode 转储文件中查找计算机名称

如果需要确定发生崩溃转储的计算机的名称，可使用 [**！ peb**](-peb.md) 扩展，并查找 COMPUTERNAME 的值它的输出。

### <a name="span-idfinding_the_ip_address_in_a_kernel_mode_dump_filespanspan-idfinding_the_ip_address_in_a_kernel_mode_dump_filespanfinding-the-ip-address-in-a-kernel-mode-dump-file"></a><span id="finding_the_ip_address_in_a_kernel_mode_dump_file"></span><span id="FINDING_THE_IP_ADDRESS_IN_A_KERNEL_MODE_DUMP_FILE"></span>查找 Kernel-Mode 转储文件中的 IP 地址

若要确定发生故障转储的计算机的 IP 地址，请找到显示某个发送/接收网络活动的线程堆栈。 打开其中一个发送数据包或接收数据包。 IP 地址将显示在该数据包中。

### <a name="span-idfinding_the_process_id_in_a_user_mode_dump_filespanspan-idfinding_the_process_id_in_a_user_mode_dump_filespanfinding-the-process-id-in-a-user-mode-dump-file"></a><span id="finding_the_process_id_in_a_user_mode_dump_file"></span><span id="FINDING_THE_PROCESS_ID_IN_A_USER_MODE_DUMP_FILE"></span>在 User-Mode 转储文件中查找进程 ID

若要确定用户模式转储文件中目标应用程序的进程 ID，请使用 [**| (进程状态)**](---process-status-.md) 命令。 这会显示在写入转储时正在调试的所有进程。 用句点 (标记的进程 **。**) 为当前进程。 其进程 ID 在 **id：** notation 后以十六进制形式提供。

 

 





