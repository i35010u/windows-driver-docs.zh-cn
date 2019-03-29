---
title: PoolMon 要求
description: PoolMon 要求
ms.assetid: 5ee1ed1c-5392-4ce4-8edb-e600b93f82d7
keywords:
- PoolMon WDK 要求
- 内存池监视器 WDK 要求
- PoolMon WDK 显示
- 内存池监视器 WDK，显示
- 文件 WDK PoolMon
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: fe393b2b7ab5da1a5fcdceefca843d9cea6df178
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575272"
---
# <a name="poolmon-requirements"></a>PoolMon 要求


## <span id="ddk_poolmon_requirements_tools"></span><span id="DDK_POOLMON_REQUIREMENTS_TOOLS"></span>


PoolMon 要求以下系统配置、 权限和文件。

### <a name="span-idsystemrequirementsspanspan-idsystemrequirementsspanspan-idsystemrequirementsspansystem-requirements"></a><span id="System_Requirements"></span><span id="system_requirements"></span><span id="SYSTEM_REQUIREMENTS"></span>系统要求

只能在 Microsoft Windows XP 和更高版本的 Windows 上运行 PoolMon 包含在 Windows Driver Kit (WDK) 中，本文档中所述的版本。

### <a name="span-idpooltaggingrequirementspanspan-idpooltaggingrequirementspanspan-idpooltaggingrequirementspanpool-tagging-requirement"></a><span id="Pool_Tagging_Requirement"></span><span id="pool_tagging_requirement"></span><span id="POOL_TAGGING_REQUIREMENT"></span>池标记要求

在 Windows XP 或更早版本的 Windows 上运行任何版本的 PoolMon 前, 必须启用池标记。 Windows Server 2003 和更高版本的 Windows 上永久启用池标记。

池标记功能收集并计算按分配的标记值的池内存有关的统计信息。

若要启用池标记，请使用 GFlags、 在有关 Windows 调试工具中包含的工具。 打开**全局标志**对话框中，选中**启用池标记**复选框，然后再重新启动计算机。

### <a name="span-idrequirementsforterminalservicessessionpoolmonitoringspanspan-idrequirementsforterminalservicessessionpoolmonitoringspanspan-idrequirementsforterminalservicessessionpoolmonitoringspanrequirements-for-terminal-services-session-pool-monitoring"></a><span id="Requirements_for_Terminal_Services_Session_Pool_Monitoring"></span><span id="requirements_for_terminal_services_session_pool_monitoring"></span><span id="REQUIREMENTS_FOR_TERMINAL_SERVICES_SESSION_POOL_MONITORING"></span>要求的终端服务会话池监视

PoolMon 显示仅在 Windows Server 2003 和更高版本的 Windows 上从终端服务会话池分配。

仅当计算机配置为终端服务器时，Windows 的终端服务会话池中分配内存。 终端服务器上的 Win32 子系统的内核模式部分的会话池中分配的内存。 否则，Windows 池内存用于终端服务从系统池分配。

### <a name="span-idrequirementsforgeneratingalocaltagfilespanspan-idrequirementsforgeneratingalocaltagfilespanspan-idrequirementsforgeneratingalocaltagfilespanrequirements-for-generating-a-local-tag-file"></a><span id="Requirements_for_Generating_a_Local_Tag_File"></span><span id="requirements_for_generating_a_local_tag_file"></span><span id="REQUIREMENTS_FOR_GENERATING_A_LOCAL_TAG_FILE"></span>生成本地标记文件的要求

**/C**参数，它创建的本地计算机上的驱动程序使用的池标记 localtag.txt 文件，仅支持 32 位版本的 Windows。

### <a name="span-iddisplayrequirementsspanspan-iddisplayrequirementsspanspan-iddisplayrequirementsspandisplay-requirements"></a><span id="Display_Requirements"></span><span id="display_requirements"></span><span id="DISPLAY_REQUIREMENTS"></span>显示要求

若要查看整个 PoolMon 显示，命令提示符窗口大小必须为至少 80 个字符宽 (宽度 = 80) 和高至少 53 行 (高度 = 53)，并且命令提示符窗口缓冲区必须至少 500 个字符宽 (宽度 = 500) 和高 （至少 2000年行高度 = 2000年)。 否则，显示可能会被截断。

### <a name="span-idrequiredfilesspanspan-idrequiredfilesspanspan-idrequiredfilesspanrequired-files"></a><span id="Required_Files"></span><span id="required_files"></span><span id="REQUIRED_FILES"></span>所需的文件

poolmon.exe

msdis130.dll

msvcp70.dll

msvcr70.dll

pooltag.txt

 

 





