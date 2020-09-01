---
title: 在 Visual Studio 中保存日志文件
description: Windows 调试器可以编写记录调试会话的日志文件。
ms.assetid: 6A7588D0-A477-4BE9-874F-3AFB52561903
ms.date: 05/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: 229af8f8c10804d1104d3459365a7864b693e8c8
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89215357"
---
# <a name="keeping-a-log-file-in-visual-studio"></a>在 Visual Studio 中保存日志文件

> [!IMPORTANT]
> 此功能在 Windows 10 版本1507及更高版本的 WDK 中不可用。
>


Windows 调试器可以编写记录调试会话的日志文件。 此日志文件包含你键入的所有命令和来自调试器的响应。 在 Microsoft Visual Studio 中，可以通过在调试器的 "即时" 窗口中输入命令来打开、追加和关闭日志文件。

本主题中所示的过程要求将 Windows 驱动程序工具包集成到 Visual Studio 中。 若要获取集成环境，请首先安装 Visual Studio，然后 (WDK) 安装 Windows 驱动程序工具包。 有关详细信息，请参阅 [Windows 驱动程序开发](../index.yml)。

## <span id="ddk_keeping_a_log_file_dbg"></span><span id="DDK_KEEPING_A_LOG_FILE_DBG"></span>


如果尚未打开调试器的 "即时" 窗口，请从 " **调试** " 菜单中选择 " ** &gt; 立即 Windows**"。

### <a name="span-idopening_a_new_log_filespanspan-idopening_a_new_log_filespanopening-a-new-log-file"></a><span id="opening_a_new_log_file"></span><span id="OPENING_A_NEW_LOG_FILE"></span>打开新的日志文件

若要打开新的日志文件，请输入 " [**logopen (打开" 日志文件) **](-logopen--open-log-file-.md) "命令。 如果你使用 **/t** 选项，则日期和时间将追加到指定的文件名。 如果使用 **/u** 选项，则以 Unicode 而不是 ASCII 编写日志文件。

### <a name="span-idappending_to_an_existing_log_filespanspan-idappending_to_an_existing_log_filespanappending-to-an-existing-log-file"></a><span id="appending_to_an_existing_log_file"></span><span id="APPENDING_TO_AN_EXISTING_LOG_FILE"></span>追加到现有日志文件

若要将文本追加到现有的日志文件，请输入 [**logpath (追加日志文件) **](-logappend--append-log-file-.md) 命令。 如果要追加到 Unicode 日志文件，必须使用 **/u** 选项。

### <a name="span-idclosing_a_log_filespanspan-idclosing_a_log_filespanclosing-a-log-file"></a><span id="closing_a_log_file"></span><span id="CLOSING_A_LOG_FILE"></span>关闭日志文件

若要关闭打开的日志文件，请输入 [**. logclose (关闭日志文件) **](-logclose--close-log-file-.md) 命令。

### <a name="span-idchecking_log_file_statusspanspan-idchecking_log_file_statusspanchecking-log-file-status"></a><span id="checking_log_file_status"></span><span id="CHECKING_LOG_FILE_STATUS"></span>正在检查日志文件状态

若要确定日志文件状态，请输入 [**.log (显示 "日志文件状态") **](-logfile--display-log-file-status-.md) 命令。

 

