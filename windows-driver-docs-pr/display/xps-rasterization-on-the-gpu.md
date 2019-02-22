---
title: 在 GPU 上的 XPS 光栅化
description: XML 纸张规范 (XPS) 光栅化 GPU 上的不需要任何独立硬件供应商 (IHV) 代码或驱动程序中的行为更改。
ms.assetid: 3C43552A-7D2B-4C10-9AD3-66755171D997
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 95436d3e791d758404b9e29672e215c7eca4620c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56542957"
---
# <a name="xps-rasterization-on-the-gpu"></a>在 GPU 上的 XPS 光栅化


XML 纸张规范 (XPS) 光栅化 GPU 上的不需要任何独立硬件供应商 (IHV) 代码或驱动程序中的行为更改。 但是，XPS 光栅化是使用模式时，可能会泄露一些 bug 或驱动程序代码中不正确的假设。 Windows 显示驱动程序模型 (WDDM) 1.2 和更高版本的驱动程序必须能够通过以确保高质量的 Windows 打印 XPS 光栅化显示符合性测试。

|                                                                                   |                                                   |
|-----------------------------------------------------------------------------------|---------------------------------------------------|
| WDDM 的最低版本                                                              | 1.2                                               |
| 最低 Windows 版本                                                           | 8                                                 |
| 驱动程序实现 — 仅完全图形和显示                              | 强制                                         |
| [WHCK](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)要求和测试 | **Device.Graphics¦XPSRasterizationConformance** |

 

## <a name="span-idxpsspanspan-idxpsspanxps-rasterization-conformance"></a><span id="xps"></span><span id="XPS"></span>XPS 光栅化符合性


XPS 光栅化显示符合性要求将确定通过 Direct2D XPS 光栅化程序上下文中使用时，WDDM 的 GPU 驱动程序是否生成正确的光栅化结果。

XPS 光栅化程序是很大程度使用栅格化 XPS 打印描述符语言 (PDL) 的 Windows 打印驱动程序的系统组件。 若要确定光栅化结果的正确性，比较之间进行从 XPS 光栅化程序的使用者 WDDM 的 GPU 驱动程序的系统上执行时获得的结果从基线使用 XPS 光栅器获得的结果.

## <a name="span-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanspan-idhardwarecertificationrequirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>硬件认证要求


有关实现此功能时，必须满足硬件设备要求的信息，请参阅相关[WHCK 文档](https://docs.microsoft.com/windows-hardware/test/hlk/windows-hardware-lab-kit)上**Device.Graphics...XPSRasterizationConformance**。

请参阅[WDDM 1.2 功能](wddm-v1-2-features.md)评审的 Windows 8 一起添加的功能。

 

 





