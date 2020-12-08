---
title: ndiskd.ndiskdversion
description: Ndiskd. ndiskdversion 扩展显示有关 ndiskd 本身的信息。
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
ms.openlocfilehash: cc1a54c982eeb3a2214853cf3cb142528f2191da
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96814063"
---
# <a name="ndiskdndiskdversion"></a>!ndiskd.ndiskdversion

**！ Ndiskd ndiskdversion** 扩展显示有关！ ndiskd 本身的信息。

```console
!ndiskd.ndiskdversion
```

## <a name="parameters"></a>参数

此扩展没有参数。

## <a name="dll"></a>DLL

Ndiskd.dll

## <a name="examples"></a>示例

下面的示例显示 **！ ndiskd. ndiskdversion** 的输出。

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

[网络驱动程序设计指南](../network/index.md)

[Windows Vista 和更高版本的网络引用](/windows-hardware/drivers/ddi/_netvista/)

[调试网络堆栈](https://channel9.msdn.com/Shows/Defrag-Tools/Defrag-Tools-175-Debugging-the-Network-Stack)

[**NDIS 扩展 ( # A0)**](ndis-extensions--ndiskd-dll-.md)

[**!ndiskd.help**](-ndiskd-help.md)
