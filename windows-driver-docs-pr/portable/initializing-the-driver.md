---
description: 初始化驱动程序
title: 初始化驱动程序
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 735fccdf1f43e77719f02983ac9de4089f81ca1a
ms.sourcegitcommit: 15caaf6d943135efcaf9975927ff3933957acd5d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/27/2020
ms.locfileid: "88968546"
---
# <a name="initializing-the-driver"></a>初始化驱动程序


在 WpdHelloWorldDriver 示例中，初始化函数 **WpdBaseDriver：： Initialize** 和 **WpdBaseDriver：：** Initialize 为空。 **Initialize**函数只返回 S \_ OK，而取消**初始化**函数不执行任何操作。

以下摘自示例驱动程序的代码包含 **WpdBaseDriver：： Initialize** 和 **WpdBaseDriver：：** Initialize 的代码。

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

如果你想要移植此示例以支持实际设备（例如启用了 Bluetooth 的移动电话），则应在 **initialize** 函数中添加功能，以便初始化驱动程序的 i/o 库。 这会发出设备命令。 对于移动电话，此库可能包含用于枚举电话簿的命令，或用于设置或检索手机存储中的文件的命令。 **Initialize**函数至少将建立设备的网络地址。 **WPDBaseDriver：：取消初始化**函数将执行任何所需的清除操作。

 

 




