---
title: MSFC \_ FIBREPORTHBAMETHODS WMI 类
description: MSFC \_ FIBREPORTHBAMETHODS WMI 类
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 316ea0a47b3f6ca6272ae8861f5d5ef0df3112d2
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96811469"
---
# <a name="msfc_fibreporthbamethods-wmi-class"></a>MSFC \_ FIBREPORTHBAMETHODS WMI 类


## <span id="ddk_msfc_fibreporthbamethods_wmi_class_kr"></span><span id="DDK_MSFC_FIBREPORTHBAMETHODS_WMI_CLASS_KR"></span>


支持 T11 委员会 *光纤通道 HBA API* 规范的 hba 微型端口驱动程序使用 MSFC \_ FibrePortHBAMethods 类公开可对光纤通道端口执行的操作。 此类仅定义了一个方法 **ResetStatistics**：

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

**ResetStatistics** 方法不需要输入或输出缓冲区。 小型端口驱动程序应执行此方法中需要的任何操作以重置端口统计信息。 每个端口都应有此类的一个实例。

 

 





