---
title: 版本
description: 版本扩展显示扩展 DLL 的版本信息。不应将此扩展命令与版本 (显示调试器版本) 命令混淆。
keywords:
- 版本 Windows 调试
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- version
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: b8a03aacf2760cee65ae366eef0f27e36dbbfa25
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96788903"
---
# <a name="version"></a>!version


**！版本** 扩展显示扩展 DLL 的版本信息。

不应将此扩展命令与 [**版本 (显示调试器版本)**](version--show-debugger-version-.md) 命令混淆。

```dbgcmd
![ExtensionDLL.]version
```

## <a name="span-idddk__version_dbgspanspan-idddk__version_dbgspanparameters"></a><span id="ddk__version_dbg"></span><span id="DDK__VERSION_DBG"></span>参数


<span id="_______ExtensionDLL______"></span><span id="_______extensiondll______"></span><span id="_______EXTENSIONDLL______"></span>*ExtensionDLL*   
指定要显示其版本号的扩展 DLL。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>.DLL

大多数扩展 Dll 中都提供此扩展。

<a name="remarks"></a>备注
-------

如果扩展 DLL 版本与调试器版本不匹配，则将显示错误消息。

此扩展命令在 Windows XP 和更高版本的 Windows 上不起作用。 若要显示版本信息，请使用 [**版本 (显示调试器版本)**](version--show-debugger-version-.md) 命令。

此扩展的原始用途是确保 DLL 版本与目标版本匹配，因为不匹配会导致很多扩展的结果不正确。 较新的 Dll 不再限制为仅使用一种版本的 Windows，因此此扩展已过时。

 

 





