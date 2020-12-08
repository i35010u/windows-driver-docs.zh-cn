---
title: DevCon Rescan
description: 使用 Windows 即插即用功能更新计算机的设备列表。 在本地和远程计算机上有效。
keywords:
- DevCon 重新扫描驱动程序开发工具
topic_type:
- apiref
api_name:
- DevCon Rescan
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2b42ba09f4dbbcc432e5c429b5cfd07b1c9d3633
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783363"
---
# <a name="devcon-rescan"></a>DevCon Rescan


使用 Windows 即插即用功能更新计算机的设备列表。 在本地和远程计算机上有效。

```
    devcon [/m:\\computer] [/r] rescan 
```

## <a name="span-idddk_devcon_rescan_toolsspanspan-idddk_devcon_rescan_toolsspanparameters"></a><span id="ddk_devcon_rescan_tools"></span><span id="DDK_DEVCON_RESCAN_TOOLS"></span>参数


<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span>**/m： \\ \\**<em>计算机</em>   
在指定的远程计算机上运行命令。 反斜杠是必需的。

**注意**   若要在远程计算机上运行 DevCon 命令，组策略设置必须允许即插即用服务在远程计算机上运行。 在运行 Windows Vista 和 Windows 7 的计算机上，默认情况下组策略禁用对服务的远程访问。 在运行 WDK 8.1 和 WDK 8 的计算机上，远程访问不可用。



<span id="________r______"></span><span id="________R______"></span>**/r**   
条件重启。 仅当需要重新启动才能使更改生效时，才能在完成操作后重新启动系统。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

**/M** 参数必须位于操作名称之前 (**重新扫描**) 。 否则，DevCon 将忽略 **/m** 参数并扫描本地计算机，而不会返回语法错误。

重新扫描可能会导致即插即用 manager 检测到新设备和安装设备驱动程序，而不发出警告。

重新扫描可以检测某些非即插即用设备，尤其是在安装时无法通知系统的设备，如并行端口设备和串行端口设备。 因此，你必须拥有管理员特权才能运行 **DevCon 重新扫描** 命令。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon rescan
devcon /m:\\Server01 rescan
```

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

[示例37：扫描计算机中的新设备](devcon-examples.md#ddk_example_37_scan_the_computer_for_new_devices_tools)









