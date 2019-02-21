---
title: DevCon 重新扫描
description: 使用 Windows 即插即用和播放功能来更新计算机的设备列表。 在本地和远程计算机上有效。
ms.assetid: 08762f30-a276-4ef4-8936-dfb1e1f692ca
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
ms.openlocfilehash: d43ef82d23d3efd96486873d83798cce1a4d8274
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56522017"
---
# <a name="devcon-rescan"></a>DevCon 重新扫描


使用 Windows 即插即用和播放功能来更新计算机的设备列表。 在本地和远程计算机上有效。

```
    devcon [/m:\\computer] [/r] rescan 
```

## <a name="span-idddkdevconrescantoolsspanspan-idddkdevconrescantoolsspanparameters"></a><span id="ddk_devcon_rescan_tools"></span><span id="DDK_DEVCON_RESCAN_TOOLS"></span>参数


<span id="________m___computer______"></span><span id="________M___COMPUTER______"></span> **/m:\\\\**<em>computer</em>   
指定远程计算机上运行该命令。 需要反斜杠。

**请注意**若要在远程计算机上运行 DevCon 命令，组策略设置必须允许 Plug and Play 服务在远程计算机上运行。 运行 Windows Vista 和 Windows 7 的计算机上，组策略默认情况下禁用远程访问服务。 运行 WDK 8.1 和 WDK 8 的计算机上，远程访问将不可用。



<span id="________r______"></span><span id="________R______"></span> **/r**   
条件性重新启动。 完成操作，仅当必须重新启动，以使更改生效后，会重新启动系统。

### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>注释

**/M**参数必须在之前的操作名称 (**重新扫描**)。 否则，将忽略 DevCon **/m**参数和本地计算机上扫描而不返回语法错误。

重新扫描可能会导致插管理器检测到新设备并安装设备驱动程序而不发出警告。

重新扫描可以检测到某些非即插设备，尤其是那些无法通知系统时安装它们，例如并行端口设备和串行端口的设备。 因此，必须拥有管理员特权才能运行**DevCon 重新扫描**命令。

### <a name="span-idsampleusagespanspan-idsampleusagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon rescan
devcon /m:\\Server01 rescan
```

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

[示例 37:扫描计算机以查找新设备](devcon-examples.md#ddk_example_37_scan_the_computer_for_new_devices_tools)









