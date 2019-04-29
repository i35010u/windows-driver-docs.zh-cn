---
title: 在 Visual Studio 中保存日志文件
description: Windows 调试器可以编写一个日志文件，用于记录调试会话。
ms.assetid: 6A7588D0-A477-4BE9-874F-3AFB52561903
ms.date: 05/11/2018
ms.localizationpriority: medium
ms.openlocfilehash: d87a58ba5c3cee9b6aa35633a8e578e3bfa0dffa
ms.sourcegitcommit: 0cc5051945559a242d941a6f2799d161d8eba2a7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/23/2019
ms.locfileid: "63367193"
---
# <a name="keeping-a-log-file-in-visual-studio"></a>在 Visual Studio 中保存日志文件

> [!IMPORTANT]
> 此功能不在 Windows 10，版本 1507年和更高版本的 WDK 中可用。
>


Windows 调试器可以编写一个日志文件，用于记录调试会话。 此日志文件包含所有的您键入的命令以及在调试器中的响应。 在 Microsoft Visual Studio 中，可以打开、 追加，并通过在调试器即时窗口中输入命令关闭日志文件。

本主题中所示的步骤要求具有集成到 Visual Studio Windows 驱动程序工具包。 要获取的集成的环境，请首先安装 Visual Studio 中，然后再安装 Windows Driver Kit (WDK)。 有关详细信息，请参阅[Windows 驱动程序开发](https://msdn.microsoft.com/library/windows/hardware/ff557573)。

## <span id="ddk_keeping_a_log_file_dbg"></span><span id="DDK_KEEPING_A_LOG_FILE_DBG"></span>


如果尚未打开，请在调试器即时窗口**调试**菜单中，选择**Windows&gt;即时**。

### <a name="span-idopeninganewlogfilespanspan-idopeninganewlogfilespanopening-a-new-log-file"></a><span id="opening_a_new_log_file"></span><span id="OPENING_A_NEW_LOG_FILE"></span>打开新的日志文件

若要打开新的日志文件，请输入[ **.logopen （打开日志文件）** ](-logopen--open-log-file-.md)命令。 如果您使用 **/t**选项，日期和时间追加到你指定的文件的名称。 如果您使用 **/u**选项，以 unicode 格式而不是 ASCII 中写入日志文件。

### <a name="span-idappendingtoanexistinglogfilespanspan-idappendingtoanexistinglogfilespanappending-to-an-existing-log-file"></a><span id="appending_to_an_existing_log_file"></span><span id="APPENDING_TO_AN_EXISTING_LOG_FILE"></span>将追加到现有日志文件

若要将文本追加到现有日志文件中，输入[ **.logappend （追加的日志文件）** ](-logappend--append-log-file-.md)命令。 如果将追加到 Unicode 日志文件，则必须使用 **/u**选项。

### <a name="span-idclosingalogfilespanspan-idclosingalogfilespanclosing-a-log-file"></a><span id="closing_a_log_file"></span><span id="CLOSING_A_LOG_FILE"></span>关闭日志文件

若要关闭打开的日志文件，请输入[ **.logclose （关闭日志文件）** ](-logclose--close-log-file-.md)命令。

### <a name="span-idcheckinglogfilestatusspanspan-idcheckinglogfilestatusspanchecking-log-file-status"></a><span id="checking_log_file_status"></span><span id="CHECKING_LOG_FILE_STATUS"></span>检查日志文件状态

若要确定日志文件状态，请输入[ **.logfile （显示日志文件状态）** ](-logfile--display-log-file-status-.md)命令。

 

 





