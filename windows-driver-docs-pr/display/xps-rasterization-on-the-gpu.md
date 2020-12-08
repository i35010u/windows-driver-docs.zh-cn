---
title: 在 GPU 上进行 XPS 光栅化
description: 用于 GPU 的 XML 纸张规范 (XPS) 光栅化不需要任何独立的硬件供应商 (IHV) 代码或驱动程序中的行为更改。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 260610971ef2b2dd5ce2ca4254556b5a74f33e0d
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96818499"
---
# <a name="xps-rasterization-on-the-gpu"></a>在 GPU 上进行 XPS 光栅化


用于 GPU 的 XML 纸张规范 (XPS) 光栅化不需要任何独立的硬件供应商 (IHV) 代码或驱动程序中的行为更改。 但是，XPS 光栅化是可能在驱动程序代码中公开 bug 或不正确假设的使用模式。 Windows 显示驱动程序模型 (WDDM) 1.2 及更高版本的驱动程序必须能够传递 XPS 光栅化显示一致性测试，以确保高质量的 Windows 打印。

**最小 WDDM 版本**：1。2

**最低 Windows 版本**：8

**驱动程序实现-完整图形和显示**：必需

**[WHCK](/windows-hardware/test/hlk/windows-hardware-lab-kit)要求和测试**： **Device. Graphics ¦ XPSRasterizationConformance**


 

## <a name="span-idxpsspanspan-idxpsspanxps-rasterization-conformance"></a><span id="xps"></span><span id="XPS"></span>XPS 光栅化一致性


XPS 光栅化显示符合性要求确定 WDDM GPU 驱动程序在 XPS 光栅化的上下文中 Direct2D 使用时是否生成正确的光栅化结果。

XPS 光栅器是 Windows 打印驱动程序广泛使用的系统组件，用于栅格化 XPS 打印描述符语言 (PDL) 。 若要确定光栅化结果的正确性，在使用 subject 的 "使用者" GPU 驱动程序的系统上执行时，将在从 XPS 光栅程序获得的结果之间进行比较，并在从 XPS 光栅化的基线使用获得的结果之间进行比较。

## <a name="span-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanspan-idhardware_certification_requirementsspanhardware-certification-requirements"></a><span id="Hardware_certification_requirements"></span><span id="hardware_certification_requirements"></span><span id="HARDWARE_CERTIFICATION_REQUIREMENTS"></span>硬件认证要求


有关硬件设备实现此功能时必须满足的要求的信息，请参阅相关 [WHCK 文档](/windows-hardware/test/hlk/windows-hardware-lab-kit) ，了解 **¦ XPSRasterizationConformance**。

请参阅 [WDDM 1.2 功能](wddm-v1-2-features.md) ，了解 Windows 8 中添加的功能。

 

