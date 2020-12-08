---
title: 创建日志文件
description: 创建日志文件
keywords:
- 日志文件 WDK 驱动程序验证程序
- 驱动程序验证程序 WDK，日志文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 69bd05f2e079a898530f76aa73ca4edb324998f2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838147"
---
# <a name="creating-log-files"></a>创建日志文件


## <span id="ddk_creating_log_files_tools"></span><span id="DDK_CREATING_LOG_FILES_TOOLS"></span>


驱动程序验证程序可以创建日志文件。 这些文件将包含与驱动程序验证程序的操作有关的统计信息的定期更新以及要验证的驱动程序的操作。

使用 **/log** 参数从验证程序实用工具创建日志文件。 还可以指定日志记录的频率。 有关详细信息，请参阅 [**Verifier 命令行**](verifier-command-line.md) 。

每个条目都包含全局计数器和单个计数器，就像验证程序 **/query** 命令一样。

有关这些统计信息的说明，请参阅 [监视全局计数器](monitoring-global-counters.md) 和 [监视单个计数器](monitoring-individual-counters.md)。

 

 





