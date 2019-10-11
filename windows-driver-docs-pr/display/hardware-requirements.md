---
title: Windows 8 中的 Direct3D 硬件要求
description: 本主题介绍在 Windows 8 中支持 Microsoft Direct3D 的硬件要求。
ms.assetid: 7297C938-D2DD-4A06-B9AD-18DDAA73A1E4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: da62c6ee2bc4e872794cdf16480b408381037974
ms.sourcegitcommit: 4bc550183bc403aee37e7aef2c38fecda1815bff
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/08/2019
ms.locfileid: "72038103"
---
# <a name="direct3d-hardware-requirements-in-windows-8"></a>Windows 8 中的 Direct3D 硬件要求


本主题介绍在 Windows 8 中支持 Microsoft Direct3D 的硬件要求。

独立硬件供应商必须遵循此表中指定的针对硬件的 Windows 8 Direct3D 呈现要求。 有关详细信息，另请参阅[Windows 8 中的 DirectX 功能改进](directx-feature-improvements-in-windows-8.md)。

**硬件的 Direct3D 呈现要求**

| Microsoft DirectX 硬件版本 | 必需/可选 | Windows 8 呈现要求 |
|------------------------------------|-------------------|----------------------------------|
| D3D9                               | 必需          | D3D9 HW 规范                     |
| D3D10                              | 必需          | D3D9 HW 规范                     |
| D3D10                              | 必需          | D3D10 HW 规范                    |
| D3D 10。1                            | 必需          | D3D9 HW 规范                     |
| D3D 10。1                            | 必需          | D3D10 HW 规范                    |
| D3D 10。1                            | 必需          | D3D 10.1 HW 规范                  |
| D3D11                              | 必需          | D3D9 HW 规范                     |
| D3D11                              | 必需          | D3D10 HW 规范                    |
| D3D11                              | 必需          | D3D 10.1 HW 规范                  |
| D3D11                              | 必需          | D3D11 HW 规范                    |
| D3D 11。1                            | 必需          | D3D9 HW 规范                     |
| D3D 11。1                            | 必需          | D3D10 HW 规范                    |
| D3D 11。1                            | 必需          | D3D 10.1 HW 规范                  |
| D3D 11。1                            | 必需          | D3D11 HW 规范                    |
| D3D 11。1                            | 必需          | D3D 11.1 HW 规范                  |

 

下表描述了适用于 Windows 8 的 Direct3D 硬件规范更新。

**适用于 Windows 8 的 Microsoft Direct3D 10 硬件规范更改**

| 是否为必需？      | 功能                            |
|----------------|------------------------------------|
| 必需       | 像素格式（5551，565，4444） \* |
| 必需       | 同一 surface blits \*              |
| 如果实现 | 逻辑操作数                          |

 

**Windows 8 的 Direct3D 10.1 硬件规范更改**

| 是否为必需？      | 功能                            |
|----------------|------------------------------------|
| 必需       | 像素格式（5551，565，4444） \* |
| 必需       | 同一 surface blits \*              |
| 如果实现 | 逻辑操作数                          |

 

**适用于 Windows 8 的 Microsoft Direct3D 11 硬件规范更改**

| 是否为必需？      | 功能                            |
|----------------|------------------------------------|
| 必需       | 像素格式（5551，565，4444） \* |
| 必需       | 同一 surface blits \*              |
| 如果实现 | UAV-MSAA                           |
| 如果实现 | 线程并发创建       |
| 如果实现 | 线程命令列表            |
| 如果实现 | 双精度支持           |
| 如果实现 | 逻辑操作数                          |

 

**Direct3D 11.1 Windows 8 硬件规范**

| 是否为必需？      | 功能                                |
|----------------|----------------------------------------|
| 必需       | 逻辑操作数                              |
| 必需       | 像素格式（5551，565，4444） \*     |
| 必需       | 同一 surface blits \*                  |
| 必需       | 每个阶段的 Uav                    |
| 必需       | UAV-MSAA                               |
| 必需       | 目标独立的光栅化 (TIR) |
| 如果实现 | 线程并发创建           |
| 如果实现 | 线程命令列表                |
| 如果实现 | 双精度支持               |

**\*** 已存在于 Microsoft Direct3D 9 硬件规范中，但以前未在 Direct3D 10 中公开。
