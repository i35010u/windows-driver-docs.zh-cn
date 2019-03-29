---
title: version
description: 版本扩展显示扩展 DLL 的版本信息。此扩展命令不应使用版本 （显示调试器版本） 命令混淆。
ms.assetid: b6ca4b8c-d673-40c5-890f-3b92fbb99fae
keywords:
- Windows 调试版本
ms.date: 05/23/2017
topic_type:
- apiref
api_name:
- version
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 2353c12fe18e72756c46d75f9ea12f3bab8ae788
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56575264"
---
# <a name="version"></a>!version


**！ 版本**扩展显示扩展 DLL 的版本信息。

不要将此扩展命令与相混淆[**版本 （显示调试器版本）** ](version--show-debugger-version-.md)命令。

```dbgcmd
![ExtensionDLL.]version
```

## <a name="span-idddkversiondbgspanspan-idddkversiondbgspanparameters"></a><span id="ddk__version_dbg"></span><span id="DDK__VERSION_DBG"></span>参数


<span id="_______ExtensionDLL______"></span><span id="_______extensiondll______"></span><span id="_______EXTENSIONDLL______"></span> *ExtensionDLL*   
指定扩展的版本编号是要显示的 DLL。

### <a name="span-iddllspanspan-iddllspandll"></a><span id="DLL"></span><span id="dll"></span>DLL

此扩展是大多数扩展 Dll 中可用。

<a name="remarks"></a>备注
-------

如果扩展 DLL 版本与调试器版本不匹配，将显示错误消息。

此扩展命令不会在 Windows XP 和更高版本的 Windows。 若要显示版本信息，请使用[**版本 （显示调试器版本）** ](version--show-debugger-version-.md)命令。

此扩展的原始用途是确保 DLL 版本匹配的目标版本中，由于不匹配会导致多个扩展插件的结果不准确。 更高版本的 Dll 不再仅限于使用只有一个版本的 Windows，因此此扩展已过时。

 

 





