---
title: 创建日志文件
description: 创建日志文件
ms.assetid: dad0f9fc-1a88-4bee-800a-5a4464fff600
keywords:
- 日志文件 WDK Driver Verifier
- 驱动程序验证程序 WDK，日志文件
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 5de449515a57945ab411524d55c6fbdeccf4b777
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522014"
---
# <a name="creating-log-files"></a>创建日志文件


## <span id="ddk_creating_log_files_tools"></span><span id="DDK_CREATING_LOG_FILES_TOOLS"></span>


驱动程序验证程序可以创建日志文件。 这些文件将包含与 Driver Verifier 的操作和要验证的驱动程序的操作相关的统计信息的一些定期更新。

日志文件通过使用创建的验证程序实用工具 **/log**参数。 还可以指定的日志记录的频率。 请参阅[**验证程序命令行**](verifier-command-line.md)有关详细信息。

每个条目将只包含全局计数器和各个计数器，如同**verifier /query**命令。

这些统计信息的说明，请参阅[监视全局计数器](monitoring-global-counters.md)并[监视各个计数器](monitoring-individual-counters.md)。

 

 





