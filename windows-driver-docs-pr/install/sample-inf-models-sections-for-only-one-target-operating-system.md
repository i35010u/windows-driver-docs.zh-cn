---
title: 只适用于一个目标操作系统的示例 INF 模型部分
description: 只适用于一个目标操作系统的示例 INF 模型部分
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 109853c93bd54a69d44b8cf16916f83fa38ef9b8
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96787357"
---
# <a name="sample-inf-models-sections-for-only-one-target-operating-system"></a>只适用于一个目标操作系统的示例 INF 模型部分


可以使用修饰的 [**INF *模型* 部分**](inf-models-section.md) 来限制适用的目标操作系统的范围。

以下示例显示了一个 [**Inf 制造商部分**](inf-manufacturer-section.md) ，其中包含各种 [**inf *模型* 部分**](inf-models-section.md) ，这些部分将阻止 Windows 在未运行 windows Vista 的基于 x86 的系统上安装设备。

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

在此示例中，" [**Inf 制造商" 部分**](inf-manufacturer-section.md) 包含以下 [**inf *模型* 部分**](inf-models-section.md)：

-   基于 x86 的系统上适用于 Windows Vista 的完整 INF *模型* 部分，其中包括设备说明和硬件标识符 (id) 。 当 windows 在运行 Windows Vista 的基于 x86 的系统上安装设备时，Windows 将选择并使用此部分。

-   任何硬件平台上适用于 Windows 7 和更高版本的 Windows 的空 INF *模式* 部分。 Windows 将选择此部分以在这些平台上安装设备。 但是，由于部分不包含任何特定的设备说明或硬件 Id，Windows 将不通过此 INF 文件安装任何设备。

 

 





