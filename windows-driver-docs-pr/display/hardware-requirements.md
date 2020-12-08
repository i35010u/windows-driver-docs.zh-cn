---
title: Windows 8 中的 Direct3D 硬件要求
description: 本主题介绍在 Windows 8 中支持 Microsoft Direct3D 的硬件要求。
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a1222f2020f7824de94bd909ac8a8b87eb964c16
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96830663"
---
# <a name="direct3d-hardware-requirements-in-windows-8"></a>Windows 8 中的 Direct3D 硬件要求


本主题介绍在 Windows 8 中支持 Microsoft Direct3D 的硬件要求。

独立硬件供应商必须遵循此表中指定的针对硬件的 Windows 8 Direct3D 呈现要求。 有关详细信息，另请参阅 [Windows 8 中的 DirectX 功能改进](directx-feature-improvements-in-windows-8.md) 。

**硬件的 Direct3D 呈现要求**

| Microsoft DirectX 硬件版本 | 必需/可选 | Windows 8 呈现要求 |
|------------------------------------|-------------------|----------------------------------|
| D3D9                               | 必须          | D3D9 HW 规范                     |
| D3D10                              | 必须          | D3D9 HW 规范                     |
| D3D10                              | 必须          | D3D10 HW 规范                    |
| D3D 10。1                            | 必须          | D3D9 HW 规范                     |
| D3D 10。1                            | 必须          | D3D10 HW 规范                    |
| D3D 10。1                            | 必须          | D3D 10.1 HW 规范                  |
| D3D11                              | 必须          | D3D9 HW 规范                     |
| D3D11                              | 必须          | D3D10 HW 规范                    |
| D3D11                              | 必须          | D3D 10.1 HW 规范                  |
| D3D11                              | 必须          | D3D11 HW 规范                    |
| D3D 11。1                            | 必须          | D3D9 HW 规范                     |
| D3D 11。1                            | 必须          | D3D10 HW 规范                    |
| D3D 11。1                            | 必须          | D3D 10.1 HW 规范                  |
| D3D 11。1                            | 必须          | D3D11 HW 规范                    |
| D3D 11。1                            | 必须          | D3D 11.1 HW 规范                  |

 

下表描述了适用于 Windows 8 的 Direct3D 硬件规范更新。

**适用于 Windows 8 的 Microsoft Direct3D 10 硬件规范更改**

| 必需？      | 功能                            |
|----------------|------------------------------------|
| 必须       | 像素格式 (5551、565、4444) \* |
| 必须       | 相同 surface blits \*              |
| 如果实现 | 逻辑操作数                          |

 

**Windows 8 的 Direct3D 10.1 硬件规范更改**

| 必需？      | 功能                            |
|----------------|------------------------------------|
| 必须       | 像素格式 (5551、565、4444) \* |
| 必须       | 相同 surface blits \*              |
| 如果实现 | 逻辑操作数                          |

 

**适用于 Windows 8 的 Microsoft Direct3D 11 硬件规范更改**

| 必需？      | 功能                            |
|----------------|------------------------------------|
| 必须       | 像素格式 (5551、565、4444) \* |
| 必须       | 相同 surface blits \*              |
| 如果实现 | UAV-MSAA                           |
| 如果实现 | 线程并发创建       |
| 如果实现 | 线程命令列表            |
| 如果实现 | 双精度支持           |
| 如果实现 | 逻辑操作数                          |

 

**Direct3D 11.1 Windows 8 硬件规范**

| 必需？      | 功能                                |
|----------------|----------------------------------------|
| 必须       | 逻辑操作数                              |
| 必须       | 像素格式 (5551、565、4444) \*     |
| 必须       | 相同 surface blits \*                  |
| 必须       | 每个阶段的 Uav                    |
| 必须       | UAV-MSAA                               |
| 必须       | 目标独立的光栅化 (TIR) |
| 如果实现 | 线程并发创建           |
| 如果实现 | 线程命令列表                |
| 如果实现 | 双精度支持               |

**\*** 已存在于 Microsoft Direct3D 9 硬件规范中，但以前未在 Direct3D 10 中公开。
