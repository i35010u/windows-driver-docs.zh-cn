---
title: 用于分析可再现问题的重要断点
description: 用于分析可再现问题的重要断点
keywords:
- SCSI 微型端口调试，断点和可重现问题
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: b0cb74860e5ae5f7e020e7207c6cae5808cefa51
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96813259"
---
# <a name="important-breakpoints-for-analyzing-reproducible-problems"></a>用于分析可再现问题的重要断点


## <span id="ddk_device_manager_problem_codes_dbg"></span><span id="DDK_DEVICE_MANAGER_PROBLEM_CODES_DBG"></span>


调试 SCSI 微型端口驱动程序时，有三个例程可用于设置断点：

-   **scsiport！ scsiportnotification**

-   **scsiport！ spstartiosynchronized**

-   **小型!HwStartIo**

在向微型端口发送请求后，将立即调用例程 **scsiport！ scsiportnotification** 。 因此，如果在 **scsiport！ scsiportnotification** 中设置了断点，然后使用 [**kb 3**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)运行堆栈 backtrace，则可以确定微型端口是否正在接收和完成请求。 如果第一个参数为零，则请求已完成。 如果第一个参数为非零值，则第三个参数是未完成 (SRB) 的 SCSI 请求块的地址，你可以使用 [**！ SRB**](-minipkd-srb.md) 扩展来进一步分析这种情况。

在 **scsiport！ spstartiosynchronized** 或微型端口中放置一个断点 **！HwStartIo** 在向微型端口发送请求之前会导致中断。

 

 





