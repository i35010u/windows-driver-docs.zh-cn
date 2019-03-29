---
title: 只适用于一个目标操作系统的示例 INF 模型部分
description: 只适用于一个目标操作系统的示例 INF 模型部分
ms.assetid: 4cad05f6-ec88-4bc8-b69a-0d6b06dfeec0
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: b1923a5f23f3e4176f8ad8585c9a2c112d01d508
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56566788"
---
# <a name="sample-inf-models-sections-for-only-one-target-operating-system"></a>只适用于一个目标操作系统的示例 INF 模型部分


可以使用修饰[ **INF*模型*各节**](inf-models-section.md)来限制适用的目标操作系统的范围。

下面的示例演示[ **INF 制造商部分**](inf-manufacturer-section.md)的各种[ **INF*模型*部分**](inf-models-section.md)将阻止 Windows 基于 x86 的系统未在运行 Windows Vista 上安装设备。

```cpp
[Manufacturer]
%Msft% = Msft, NTx86.6.0, NT.6.1

;For Windows Vista only

[Msft.NTx86.6.0]
%NetVMini.DeviceDesc%    = NetVMini.ndi, root\NetVMini ; Root enumerated 
%NetVMini.DeviceDesc%    = NetVMini.ndi, {b85b7c50-6a01-11d2-b841-00c04fad5171}\NetVMini ; Toaster Bus enumerated 

;For Windows 7 and later

[Msft.NT.6.1]
```

在此示例中， [ **INF 制造商部分**](inf-manufacturer-section.md)具有以下[ **INF*模型*部分**](inf-models-section.md):

-   完整 INF*模型*适用于 Windows Vista 包括设备描述和硬件标识符 (Id) 的基于 x86 的系统上的部分。 Windows 将选择并安装在设备上运行的 Windows Vista 的基于 x86 的系统时使用此部分。

-   空 INF*模型*部分，了解 Windows 7 和更高版本 Windows 的任何硬件平台上。 Windows 将选择在这些平台上的设备安装的此部分。 但是，由于部分包含任何特定设备说明或硬件 Id，Windows 将不安装任何设备通过此 INF 文件。

 

 





