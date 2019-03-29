---
title: 从转储文件中提取信息
description: 从转储文件中提取信息
ms.assetid: abde266e-e3ab-4e5e-ac6d-a27933f3d1a9
keywords:
- 从转储文件中提取信息
- 解压缩的各种信息的转储文件
- （确定从转储文件） 的计算机名称
- （确定从转储文件） 的计算机名称
- （确定从转储文件） 的 IP 地址
ms.date: 03/13/2019
ms.localizationpriority: medium
ms.openlocfilehash: 534c208507ed2c07e233984b3a159fac8fc82854
ms.sourcegitcommit: 71938460f3d04caa4b4d6d0cee695db887ee35e8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/19/2019
ms.locfileid: "57909200"
---
# <a name="extracting-information-from-a-dump-file"></a>从转储文件中提取信息


## <span id="ddk_extracting_information_from_a_dump_file_dbg"></span><span id="DDK_EXTRACTING_INFORMATION_FROM_A_DUMP_FILE_DBG"></span>


在实时调试期间，某些种类的信息，如目标计算机的名称就能轻松访问。 调试转储文件时需要一些额外工作来确定此信息。

### <a name="span-idfindingthecomputernameinakernelmodedumpfilespanspan-idfindingthecomputernameinakernelmodedumpfilespanfinding-the-computer-name-in-a-kernel-mode-dump-file"></a><span id="finding_the_computer_name_in_a_kernel_mode_dump_file"></span><span id="FINDING_THE_COMPUTER_NAME_IN_A_KERNEL_MODE_DUMP_FILE"></span>内核模式转储文件中查找计算机名称

如果您需要确定在其进行了故障转储的计算机的名称，则可以使用[ **！ peb** ](-peb.md)扩展和查找的值的 COMPUTERNAME 它其输出。

### <a name="span-idfindingtheipaddressinakernelmodedumpfilespanspan-idfindingtheipaddressinakernelmodedumpfilespanfinding-the-ip-address-in-a-kernel-mode-dump-file"></a><span id="finding_the_ip_address_in_a_kernel_mode_dump_file"></span><span id="FINDING_THE_IP_ADDRESS_IN_A_KERNEL_MODE_DUMP_FILE"></span>内核模式转储文件中查找的 IP 地址

若要确定其进行了故障转储的计算机的 IP 地址，请找到显示某些发送/接收网络活动的线程堆栈。 打开一个发送数据包或接收数据包。 IP 地址将是该数据包中可见。

### <a name="span-idfindingtheprocessidinausermodedumpfilespanspan-idfindingtheprocessidinausermodedumpfilespanfinding-the-process-id-in-a-user-mode-dump-file"></a><span id="finding_the_process_id_in_a_user_mode_dump_file"></span><span id="FINDING_THE_PROCESS_ID_IN_A_USER_MODE_DUMP_FILE"></span>在用户模式转储文件中查找的进程 ID

若要确定用户模式转储文件的目标应用程序的进程 ID，请使用[ **|（进程状态）** ](---process-status-.md)命令。 这将显示在写入转储时正在调试的所有进程。 该过程标记为以句点 (**。**) 是当前进程。 以十六进制后给出其进程 ID **id:** 表示法。

 

 





