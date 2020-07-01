---
title: ndiskd.ndiskdversion
description: Ndiskd. ndiskdversion 扩展显示有关 ndiskd 本身的信息。
ms.assetid: 12EB9E0F-7D2F-447B-B678-1E23EFF522FE
keywords:
- ndiskd ndiskdversion Windows 调试
ms.date: 06/11/2020
topic_type:
- apiref
api_name:
- ndiskd.ndiskdversion
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: 887ff00c3e2a277862de67aade636184358d489d
ms.sourcegitcommit: 8596782b07c8a71adf38fc2c2da68b75ba0a1259
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/01/2020
ms.locfileid: "85593927"
---
# <a name="ndiskdndiskdversion"></a>!ndiskd.ndiskdversion

**！ Ndiskd ndiskdversion**扩展显示有关！ ndiskd 本身的信息。

```console
!ndiskd.ndiskdversion
```

## <a name="parameters"></a>参数

此扩展没有参数。

## <a name="dll"></a>DLL

Ndiskd.dll

## <a name="examples"></a>示例

下面的示例显示 **！ ndiskd. ndiskdversion**的输出。

```console
0: kd> !ndiskd.ndiskdversion
    NDISKD Version     17.08.00 (NDISKD codename "We'll deploy IPv6 real soon now")
    Build              Release
    Debugger CPU       AMD64
    Hyperlinks (DML)   Enabled
    Unicode            Enabled
    Debug NDISKD       Disabled
```

## <a name="see-also"></a>请参阅

[网络驱动程序设计指南](https://docs.microsoft.com/windows-hardware/drivers/network/index)

[Windows Vista 和更高版本的网络引用](https://docs.microsoft.com/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展（Ndiskd.dll）**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)
