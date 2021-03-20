---
title: MB 收集日志
description: MB 收集日志
ms.date: 03/10/2021
ms.localizationpriority: medium
ms.openlocfilehash: ca0ce80faff6143a014426575c76337d992d52b7
ms.sourcegitcommit: 76a7b604f13cf419ff21518337913820a703347f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2021
ms.locfileid: "104719546"
---
# <a name="mobilebroadband-collecting-logs"></a>MobileBroadband 收集日志

按照以下步骤收集 Windows 桌面设备上与 Mobilebroadband 相关的日志：
```
*  Open an Administrator Command Prompt window
*  Run the below command to start tracing
    *  netsh trace start wireless_dbg,provisioning overwrite=yes maxSize=999
*  <Repro the scenario for which you need to collect logs>
*  Run the below command to stop tracing
    *  netsh trace stop
```
以上步骤会生成两个文件：
1.  NetTrace-包含运行的跟踪
2.  NetTrace.cab-包含有关可用于调试的系统的其他详细信息

## <a name="collecting-logs-across-a-reboot"></a>跨重启收集日志

如果重现方案包括 "重新启动"，请更新 start 跟踪命令，如下所示：
```
*  netsh trace start wireless_dbg,provisioning overwrite=yes persist=yes level=5
```

**请注意，将使用以上方法收集的日志中捕获 PII。**

## <a name="decoding-logs"></a>解码日志

运行以下命令之一，将 .etl 文件转换为可用于分析的 .txt 文件：

  ```*  ```[```tracefmt```](../devtest/tracefmt-commands.md)``` <ETL file location>  ```<br/>
  ```    or ```<br/>
  ```*  netsh trace convert <ETL file location>```
