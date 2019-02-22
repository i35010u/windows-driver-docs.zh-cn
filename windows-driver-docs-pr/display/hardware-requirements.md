---
title: 在 Windows 8 中的 Direct3D 硬件要求
description: 本主题介绍在 Windows 8 中支持 Microsoft Direct3D 硬件要求。
ms.assetid: 7297C938-D2DD-4A06-B9AD-18DDAA73A1E4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 130268432a805b92fed9cf90a644fbd19b2bbb9c
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56554094"
---
# <a name="direct3d-hardware-requirements-in-windows-8"></a>在 Windows 8 中的 Direct3D 硬件要求


本主题介绍在 Windows 8 中支持 Microsoft Direct3D 硬件要求。

独立硬件供应商必须遵循 Windows 8 Direct3D 呈现要求的硬件，此表中指定。 另请参阅[Windows 8 中的 DirectX 功能改进措施](directx-feature-improvements-in-windows-8.md)了解详细信息。

**Direct3D 呈现的硬件要求**

| Microsoft DirectX 硬件版本 | 必需/可选 | Windows 8 的渲染要求 |
|------------------------------------|-------------------|----------------------------------|
| D3D9                               | 必需          | D3D9 硬件规范                     |
| D3D10                              | 必需          | D3D9 硬件规范                     |
| D3D10                              | 必需          | D3D10 硬件规范                    |
| D3D10.1                            | 必需          | D3D9 硬件规范                     |
| D3D10.1                            | 必需          | D3D10 硬件规范                    |
| D3D10.1                            | 必需          | D3D10.1 硬件规范                  |
| D3D11                              | 必需          | D3D9 硬件规范                     |
| D3D11                              | 必需          | D3D10 硬件规范                    |
| D3D11                              | 必需          | D3D10.1 硬件规范                  |
| D3D11                              | 必需          | D3D11 HW Spec                    |
| D3D11.1                            | 必需          | D3D9 硬件规范                     |
| D3D11.1                            | 必需          | D3D10 硬件规范                    |
| D3D11.1                            | 必需          | D3D10.1 硬件规范                  |
| D3D11.1                            | 必需          | D3D11 HW Spec                    |
| D3D11.1                            | 必需          | D3D11.1 硬件规范                  |

 

下表描述适用于 Windows 8 的 Direct3D 硬件规范更新。

**Microsoft Direct3D 10 的 Windows 8 的硬件规范更改**

| 是否为必需？      | 功能                            |
|----------------|------------------------------------|
| 必需       | 像素格式 (5551，565、 4444) \* |
| 必需       | 同一个面 blits \*              |
| 如果实现 | 逻辑操作                          |

 

**Windows 8 的 Direct3D 10.1 硬件规范更改**

| 是否为必需？      | 功能                            |
|----------------|------------------------------------|
| 必需       | 像素格式 (5551，565、 4444) \* |
| 必需       | 同一个面 blits \*              |
| 如果实现 | 逻辑操作                          |

 

**Windows 8 的 Microsoft Direct3D 11 硬件规范更改**

| 是否为必需？      | 功能                            |
|----------------|------------------------------------|
| 必需       | 像素格式 (5551，565、 4444) \* |
| 必需       | 同一个面 blits \*              |
| 如果实现 | UAV-MSAA                           |
| 如果实现 | 线程处理并发创建       |
| 如果实现 | 线程处理的命令列表            |
| 如果实现 | 双精度支持           |
| 如果实现 | 逻辑操作                          |

 

**Windows 8 的 Direct3D 11.1 硬件规范**

| 是否为必需？      | 功能                                |
|----------------|----------------------------------------|
| 必需       | 逻辑操作                              |
| 必需       | 像素格式 (5551，565、 4444) \*     |
| 必需       | 同一个面 blits \*                  |
| 必需       | 在每个阶段的 Uav                    |
| 必需       | UAV-MSAA                               |
| 必需       | 独立于目标的光栅化 (TIR) |
| 如果实现 | 线程处理并发创建           |
| 如果实现 | 线程处理的命令列表                |
| 如果实现 | 双精度支持               |

 

**\\*** 已存在于 Microsoft Direct3D 9 的硬件规范，但以前未在 Direct3D 10 中公开。

 

 





