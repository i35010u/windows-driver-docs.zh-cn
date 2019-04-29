---
title: 用于分析可再现问题的重要断点
description: 用于分析可再现问题的重要断点
ms.assetid: 3f501bbe-990a-4f46-ba88-c1fc4b73537f
keywords:
- SCSI 微型端口调试、 断点和可重现问题
ms.date: 05/23/2017
ms.localizationpriority: medium
ms.openlocfilehash: e9f4247798cf2e43288c956ddff66749fb06bf2f
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63371658"
---
# <a name="important-breakpoints-for-analyzing-reproducible-problems"></a>用于分析可再现问题的重要断点


## <span id="ddk_device_manager_problem_codes_dbg"></span><span id="DDK_DEVICE_MANAGER_PROBLEM_CODES_DBG"></span>


在调试时 SCSI 微型端口驱动程序，有三个例程，它是用于设置断点：

-   **scsiport!scsiportnotification**

-   **scsiport!spstartiosynchronized**

-   **miniport!HwStartIo**

例程**scsiport ！ scsiportnotification**后将请求发送到微型端口直接调用。 因此，如果在中设置断点**scsiport ！ scsiportnotification** ，然后运行堆栈回溯使用[ **kb 3**](k--kb--kc--kd--kp--kp--kv--display-stack-backtrace-.md)，可以确定微型端口是否正在接收和完成请求。 如果第一个参数为零，表示已完成请求。 如果第一个参数为非零值，第三个参数是没有按时完成的 SCSI 请求块 (SRB) 的地址，可以使用[ **！ minipkd.srb** ](-minipkd-srb.md)扩展，若要进一步分析情形。

将断点放置在**scsiport ！ spstartiosynchronized**或**微型端口 ！HwStartIo**会导致之前向微型端口发送请求一个分行符。

 

 





