---
title: 有关自定义功能的常见问题解答
description: 介绍用于硬件支持的应用 (HSA) 以及它们之间的区别于其他功能的自定义功能。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 432e205c52bb9cd5617ab2cb3f024ae7b8adab7a
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56533767"
---
# <a name="faq-on-custom-capabilities"></a>有关自定义功能的常见问题解答

## <a name="how-are-custom-capabilities-different-from-other-capabilities"></a>如何自定义功能是否不同于其他功能？

1. Microsoft 合作伙伴可以定义自定义功能。
2. 自定义功能无需内置于 Windows 在编译时。
3. Windows 验证应用程序有权在安装应用时使用自定义功能。  对于其他功能，此验证 Windows 应用商店接收应用程序提交时发生。

## <a name="whats-the-difference-between-uwp-apps-with-custom-capabilities-and-device-companion-apps-dcas"></a>具有自定义功能的 UWP 应用与设备配套应用程序 (DCAs) 之间的区别是什么？

|                           | **DCA**                                                  | **UWP 应用，而自定义功能**|
|---------------------------|----------------------------------------------------------|-------------------------------------|
|通信|设备方案 API （映像捕获，扫描，等等。）<br>设备协议 Api （如 USB、 HID 等）。<br>客户驱动程序访问权限|                                                                              
|信任模型|在"容器"级别定义<br>系统的 OEM 必须提交适用于内部组件的应用|在系统级别上定义<br>系统的 OEM 必须提交适用于内部组件的应用|
|获取自动应用程序  |适用于外围设备                                  |适用于所有硬件          |
|部署依赖关系    |WU:驱动程序包<br>存储：应用|WU:驱动程序包<br>存储：应用                  |
                                                                                                                                                                                                    
DCAs 的详细信息，请参阅[开始使用 Microsoft Store 的设备应用程序](https://msdn.microsoft.com/windows/hardware/drivers/devapps/getting-started)。

