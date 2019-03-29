---
title: 为虚拟功能释放资源
description: 为虚拟功能释放资源
ms.assetid: 48FACA22-69B2-456C-9009-3CA42DE94FC4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 340a77abc2da974a4e0c12ed8bdfe9bddf0b58ff
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56576310"
---
# <a name="freeing-resources-for-a-virtual-function"></a>为虚拟功能释放资源


基础驱动程序会请求资源分配的 PCI Express (PCIe) 虚拟函数 (VF) 的对象标识符 (OID) 的方法请求通过[OID\_NIC\_交换机\_分配\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451814). 基础驱动程序已成功分配 VF 资源后，释放通过 OID 集请求的资源[OID\_NIC\_交换机\_免费\_VF](https://msdn.microsoft.com/library/windows/hardware/hh451822)。

本部分包括以下主题：

[发出 OID\_NIC\_交换机\_免费\_VF 请求](issuing-oid-nic-switch-allocate-vf-requests.md)

[处理 OID\_NIC\_交换机\_免费\_VF 请求](handling-oid-nic-switch-allocate-vf-requests.md)

 

 





