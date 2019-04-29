---
title: 在 KD 中保存日志文件
description: 在 KD 中保存日志文件
ms.assetid: 8A260D7F-5E05-4DD0-9CDF-56D3A0C4C2B6
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 7a6f4641943421c938b4e9cf9088c91688d89d7a
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367196"
---
# <a name="keeping-a-log-file-in-kd"></a>在 KD 中保存日志文件


## <span id="ddk_keeping_a_log_file_dbg"></span><span id="DDK_KEEPING_A_LOG_FILE_DBG"></span>


KD 可以编写一个日志文件，用于记录调试会话。 此日志文件包含所有的您键入的命令以及在调试器中的响应。

### <a name="span-idopeninganewlogfilespanspan-idopeninganewlogfilespanopening-a-new-log-file"></a><span id="opening_a_new_log_file"></span><span id="OPENING_A_NEW_LOG_FILE"></span>打开新的日志文件

若要打开一个新的日志文件，或覆盖以前的日志文件，请执行以下操作：

-   启动调试器之前，设置\_NT\_调试\_日志\_文件\_打开[环境变量](environment-variables.md)。

-   当您启动调试器时，使用 **-徽标**命令行选项。

-   输入[ **.logopen （打开日志文件）** ](-logopen--open-log-file-.md)命令。 如果您使用 **/t**选项，日期和时间追加到你指定的文件的名称。 如果您使用 **/u**选项，以 unicode 格式而不是 ASCII 中写入日志文件。

### <a name="span-idappendingtoanexistinglogfilespanspan-idappendingtoanexistinglogfilespanappending-to-an-existing-log-file"></a><span id="appending_to_an_existing_log_file"></span><span id="APPENDING_TO_AN_EXISTING_LOG_FILE"></span>将追加到现有日志文件

若要将文本追加到现有日志文件，请执行以下操作：

-   启动调试器之前，设置\_NT\_调试\_日志\_文件\_追加[环境变量](environment-variables.md)。

-   当您启动调试器时，使用 **-loga**命令行选项。

-   输入[ **.logappend （追加的日志文件）** ](-logappend--append-log-file-.md)命令。 如果将追加到 Unicode 日志文件，则必须使用 **/u**选项。

### <a name="span-idclosingalogfilespanspan-idclosingalogfilespanclosing-a-log-file"></a><span id="closing_a_log_file"></span><span id="CLOSING_A_LOG_FILE"></span>关闭日志文件

若要关闭打开的日志文件，请执行以下操作：

-   输入[ **.logclose （关闭日志文件）** ](-logclose--close-log-file-.md)命令。

### <a name="span-idcheckinglogfilestatusspanspan-idcheckinglogfilestatusspanchecking-log-file-status"></a><span id="checking_log_file_status"></span><span id="CHECKING_LOG_FILE_STATUS"></span>检查日志文件状态

若要确定日志文件状态，请执行以下操作：

-   输入[ **.logfile （显示日志文件状态）** ](-logfile--display-log-file-status-.md)命令。

 

 





