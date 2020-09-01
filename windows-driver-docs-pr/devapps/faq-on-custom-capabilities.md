---
title: 自定义功能常见问题
description: 介绍 (HSA) 的硬件支持应用的自定义功能，以及它们与其他功能有何不同。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 0c2451af5824c2880979a5a0e2ac9bb91c620206
ms.sourcegitcommit: 4db5f9874907c405c59aaad7bcc28c7ba8280150
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/29/2020
ms.locfileid: "89097039"
---
# <a name="faq-on-custom-capabilities"></a>自定义功能常见问题

## <a name="how-are-custom-capabilities-different-from-other-capabilities"></a>自定义功能与其他功能有何不同？

1. Microsoft 合作伙伴可以定义自定义功能。
2. 在编译时，无需内置于 Windows 中的自定义功能。
3. Windows 验证应用是否有权在应用安装时使用自定义功能。  对于其他功能，Windows 应用商店接收应用提交时会发生此验证。

## <a name="whats-the-difference-between-uwp-apps-with-custom-capabilities-and-device-companion-apps-dcas"></a>具有自定义功能和设备助理应用 (DCAs) 的 UWP 应用之间有何区别？

|                           | **DCA**                                                  | **具有自定义功能的 UWP 应用**|
|---------------------------|----------------------------------------------------------|-------------------------------------|
|通信|设备方案 API (映像捕获、扫描等 ) <br>设备协议 Api (USB、HID 等 ) <br>客户驱动程序访问|                                                                              
|信任模型|在 "容器" 级别定义<br>系统的 OEM 必须提交内部组件应用|在系统级别定义<br>系统的 OEM 必须提交内部组件应用|
|自动应用获取  |适用于外设                                  |适用于所有硬件          |
|部署依赖关系    |WU：驱动程序包<br>应用商店：应用|WU：驱动程序包<br>应用商店：应用                  |
                                                                                                                                                                                                    
有关 DCAs 的详细信息，请参阅 [Microsoft Store 设备应用](./getting-started.md)入门。