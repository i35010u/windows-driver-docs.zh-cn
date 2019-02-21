---
title: MSFC\_FibrePortHBAMethods WMI 类
description: MSFC\_FibrePortHBAMethods WMI 类
ms.assetid: 7c9f5c94-0c50-4a7a-b05e-41e93409d1e3
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: a34c437755478a3ef9d6ed145daccee9b43960e4
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520889"
---
# <a name="msfcfibreporthbamethods-wmi-class"></a>MSFC\_FibrePortHBAMethods WMI 类


## <span id="ddk_msfc_fibreporthbamethods_wmi_class_kr"></span><span id="DDK_MSFC_FIBREPORTHBAMETHODS_WMI_CLASS_KR"></span>


HBA 微型端口驱动程序支持 T11 委员会*光纤通道 HBA API*规范使用 MSFC\_FibrePortHBAMethods 类公开的光纤通道端口可以执行的操作。 此类定义只是一种方法， **ResetStatistics**:

```cpp
class MSFC_FibrePortHBAMethods
{
    [key] 
    string InstanceName;
    boolean Active;
    [ Implemented, WmiMethodId(1)]
    void ResetStatistics();
};
```

**ResetStatistics**方法需要任何输入或输出缓冲区。 微型端口驱动程序应执行任何内容是在这种方法重置所需端口统计信息。 应为每个端口的此类的一个实例。

 

 





