---
title: PoolMon 要求
description: PoolMon 要求
keywords:
- PoolMon WDK，要求
- 内存池监视 WDK，要求
- PoolMon WDK，显示
- 内存池监视器 WDK，显示
- 文件 WDK PoolMon
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 84a19034d3046fcf5ae0be7eea6d16d4f8793881
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96841013"
---
# <a name="poolmon-requirements"></a>PoolMon 要求


## <span id="ddk_poolmon_requirements_tools"></span><span id="DDK_POOLMON_REQUIREMENTS_TOOLS"></span>


PoolMon 需要以下系统配置、权限和文件。

### <a name="span-idsystem_requirementsspanspan-idsystem_requirementsspanspan-idsystem_requirementsspansystem-requirements"></a><span id="System_Requirements"></span><span id="system_requirements"></span><span id="SYSTEM_REQUIREMENTS"></span>系统要求

Windows 驱动程序工具包中包含的 PoolMon 版本 (WDK) 并在本文档中所述仅在 Microsoft Windows XP 和更高版本的 Windows 上运行。

### <a name="span-idpool_tagging_requirementspanspan-idpool_tagging_requirementspanspan-idpool_tagging_requirementspanpool-tagging-requirement"></a><span id="Pool_Tagging_Requirement"></span><span id="pool_tagging_requirement"></span><span id="POOL_TAGGING_REQUIREMENT"></span>池标记要求

在 Windows XP 或更早版本的 Windows 上运行 PoolMon 的任何版本之前，必须启用池标记。 在 Windows Server 2003 和更高版本的 Windows 上永久启用池标记。

池标记功能收集和计算按分配的标记值排序的池内存的统计信息。

若要启用池标记，请使用 GFlags，它是 Windows 调试工具中包含的工具。 打开 " **全局标志** " 对话框，选中 " **启用池标记** " 复选框，然后重新启动计算机。

### <a name="span-idrequirements_for_terminal_services_session_pool_monitoringspanspan-idrequirements_for_terminal_services_session_pool_monitoringspanspan-idrequirements_for_terminal_services_session_pool_monitoringspanrequirements-for-terminal-services-session-pool-monitoring"></a><span id="Requirements_for_Terminal_Services_Session_Pool_Monitoring"></span><span id="requirements_for_terminal_services_session_pool_monitoring"></span><span id="REQUIREMENTS_FOR_TERMINAL_SERVICES_SESSION_POOL_MONITORING"></span>终端服务会话池监视的要求

PoolMon 仅显示来自 Windows Server 2003 和更高版本的 Windows 上的终端服务会话池的分配。

仅当计算机配置为终端服务器时，Windows 才从终端服务会话池分配内存。 在终端服务器上，Win32 子系统的内核模式部分从会话池分配内存。 否则，Windows 将从系统池中为终端服务分配池内存。

### <a name="span-idrequirements_for_generating_a_local_tag_filespanspan-idrequirements_for_generating_a_local_tag_filespanspan-idrequirements_for_generating_a_local_tag_filespanrequirements-for-generating-a-local-tag-file"></a><span id="Requirements_for_Generating_a_Local_Tag_File"></span><span id="requirements_for_generating_a_local_tag_file"></span><span id="REQUIREMENTS_FOR_GENERATING_A_LOCAL_TAG_FILE"></span>生成本地标记文件的要求

**/C** 参数用于创建本地计算机上的驱动程序所使用的池标记 localtag.txt 文件，仅在32位版本的 Windows 上受支持。

### <a name="span-iddisplay_requirementsspanspan-iddisplay_requirementsspanspan-iddisplay_requirementsspandisplay-requirements"></a><span id="Display_Requirements"></span><span id="display_requirements"></span><span id="DISPLAY_REQUIREMENTS"></span>显示要求

若要查看整个 PoolMon 显示，"命令提示符" 窗口大小必须至少为80个字符宽 (width = 80) ，至少53行高 (height = 53) ，并且命令提示符窗口缓冲区必须至少为500个字符宽 (width = 500) 并且至少2000行高 (height = 2000) 。 否则，显示可能会被截断。

### <a name="span-idrequired_filesspanspan-idrequired_filesspanspan-idrequired_filesspanrequired-files"></a><span id="Required_Files"></span><span id="required_files"></span><span id="REQUIRED_FILES"></span>必需的文件

poolmon.exe

msdis130.dll

msvcp70.dll

msvcr70.dll

pooltag.txt

 

 





