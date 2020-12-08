---
title: DevCon Reboot
description: 停止然后启动操作系统。 仅在本地计算机上有效。
keywords:
- DevCon 重新启动驱动程序开发工具
topic_type:
- apiref
api_name:
- DevCon Reboot
api_type:
- NA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b625f651ba3bb0d659235ee063eec9d68270e52b
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96783373"
---
# <a name="devcon-reboot"></a>DevCon Reboot


停止然后启动操作系统。 仅在本地计算机上有效。

```
    devcon reboot 
```

## <span id="ddk_devcon_reboot_tools"></span><span id="DDK_DEVCON_REBOOT_TOOLS"></span>


### <a name="span-idcommentsspanspan-idcommentsspancomments"></a><span id="comments"></span><span id="COMMENTS"></span>提出

与 **/r** 参数不同，后者仅在必要时才重新启动系统以使更改生效， **DevCon reboot** 操作会重新启动系统而不确定是否需要重新启动。

DevCon 使用标准的 **ExitWindowsEx** 函数来重新启动。 如果用户在计算机上有打开的文件，或程序不会关闭，则系统不会重新启动，直到用户响应系统提示以关闭文件或结束进程。 有关 **ExitWindowsEx** 的详细信息，请参阅 Microsoft Windows SDK。

### <a name="span-idsample_usagespanspan-idsample_usagespansample-usage"></a><span id="sample_usage"></span><span id="SAMPLE_USAGE"></span>示例用法

```
devcon reboot
```

### <a name="span-idexamplespanspan-idexamplespanexample"></a><span id="example"></span><span id="EXAMPLE"></span>示例

[示例39：重新启动本地计算机](devcon-examples.md#ddk_example_39_reboot_the_local_computer_tools)









