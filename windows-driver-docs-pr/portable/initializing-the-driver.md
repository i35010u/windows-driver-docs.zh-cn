---
Description: Initializing the Driver
title: 初始化驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: e6145c0b10ae249d1335753ddcdf1f7b86593d14
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56520086"
---
# <a name="initializing-the-driver"></a>初始化驱动程序


初始化函数， **WpdBaseDriver::Initialize**并**WpdBaseDriver::Uninitialize** WpdHelloWorldDriver 示例中为空。 **初始化**函数只需返回 S\_确定和**Uninitialize**函数不执行任何操作。

以下内容摘自示例驱动程序包含的代码**WpdBaseDriver::Initialize**并**WpdBaseDriver::Uninitialize**。

```ManagedCPlusPlus
/**
 * This method is called to initialize the driver object.
 * This is where the driver would set up its I/O libraries
 * and so on.
 */
HRESULT WpdBaseDriver::Initialize()
{

    return S_OK;
}

/**
 * This method is called to uninitialize the driver object.
 * In a real driver, this is where the driver would clean up
 * any resources held by this driver.
 */
VOID WpdBaseDriver::Uninitialize()
{
}
```

如果你想要移植此示例，以支持在真实设备 — 例如，已启用蓝牙的移动电话-添加中的功能**初始化**函数以初始化驱动程序的 I/O 库。 哪些问题设备的命令。 在移动电话的情况下此库可能包括命令枚举电话薄，或者要设置或检索手机的存储中的文件。 在最低限度**初始化**函数会建立设备的网络地址。 **WPDBaseDriver::Uninitialize**函数会执行任何所需的清理。

 

 




