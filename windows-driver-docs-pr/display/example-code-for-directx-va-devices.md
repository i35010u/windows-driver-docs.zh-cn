---
title: DirectX VA 设备的示例代码
description: DirectX VA 设备的示例代码
keywords:
- DirectX 视频加速 WDK Windows 2000 显示，示例代码
- 视频加速 WDK DirectX，示例代码
- VA WDK DirectX，示例代码
- 示例 WDK DirectX VA
- 模板 WDK DirectX VA
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 270446dad9929a5a2a5c6a626debfc0fbef64922
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838311"
---
# <a name="example-code-for-directx-va-devices"></a>DirectX VA 设备的示例代码


## <span id="ddk_example_code_for_directx_va_devices_gg"></span><span id="DDK_EXAMPLE_CODE_FOR_DIRECTX_VA_DEVICES_GG"></span>


本部分中提供的示例代码显示了 [运动补偿](motion-compensation-callbacks.md) 代码模板的实现以及已认证的输出保护协议 (COPP) 视频微型端口驱动程序模板。 运动补偿代码模板用于访问 ProcAmp 控制、取消隔行扫描和 COPP 功能。 COPP 视频微型端口驱动程序模板用于访问 COPP 功能。 使用这些模板可以简化显示器驱动程序和视频微型端口驱动程序的开发。 但是，你无需以这种方式实现对 ProcAmp control、取消隔行扫描和 COPP 功能的访问，这样你的驱动程序就能正常工作。

本节包括：

[运动补偿代码模板](motion-compensation-code-template.md)

[COPP 视频微型端口驱动程序模板](copp-video-miniport-driver-template.md)

 

 





