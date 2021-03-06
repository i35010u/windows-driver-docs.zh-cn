---
title: MBIMEx 3.0 – 5G SA 第1阶段支持
description: MBIMEx 3.0 – 5G SA 第1阶段支持
keywords:
- MBIMEx 3.0 – 5G SA 第1阶段支持
ms.date: 03/01/2021
ms.localizationpriority: medium
ms.openlocfilehash: 2740fba34696097a65d54cbce8ee82713c52c040
ms.sourcegitcommit: a9fb2c30adf09ee24de8e68ac1bc6326ef3616b8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/06/2021
ms.locfileid: "102250423"
---
# <a name="mbimex-30--5g-sa-phase-1-support"></a>MBIMEx 3.0 – 5G SA 第1阶段支持

从 Windows 10 版本21H1 开始，Windows OS 支持下一代核心网络的5G 系统的第一阶段功能。 这些5G 系统通常称为 5G SA 网络。 它们包含新的 5G Core Network (5GC) ，与 5G NSA 网络和4G 网络中使用的增强型数据包核心 (EPC) 无关。  

与 5G NSA 相比，5G SA 的第一阶段功能在 5G SA 网络上启用 Windows MBIM MBB 设备的 MBB 功能奇偶校验。 这些功能包括在默认 eMBB 网络片上注册5GC 和基本 PDU 会话。 请注意，此阶段不支持更高级的 5G SA 功能，如多个并发网络切片和 URSP 规则。

为 MBIM 接口中的更改引入了新的 MBIM 扩展版本3.0，以支持 5G SA 的第一阶段功能。 此扩展发布号通常称为 MBIMEx 3.0。 [在此处下载 MBIMEx 3.0 规范](https://download.microsoft.com/download/8/3/a/83a64106-a1f4-4a03-811f-4dbef2e3bf7a/MBIM%20extensions%20for%205G.docx)。
