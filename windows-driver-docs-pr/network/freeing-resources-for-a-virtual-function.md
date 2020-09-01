---
title: 为虚拟功能释放资源
description: 为虚拟功能释放资源
ms.assetid: 48FACA22-69B2-456C-9009-3CA42DE94FC4
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: f6db5efe7c9c116b9aa248db519099c73c1124a9
ms.sourcegitcommit: f500ea2fbfd3e849eb82ee67d011443bff3e2b4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/31/2020
ms.locfileid: "89212463"
---
# <a name="freeing-resources-for-a-virtual-function"></a>为虚拟功能释放资源


过量驱动程序通过对象标识符 (PCIe) 虚函数请求资源分配 (VF) ， (OID [ \_ NIC \_ 交换机 \_ 分配 \_ VF](./oid-nic-switch-allocate-vf.md)的方法请求。 成功分配 VF 资源后，过量驱动程序将通过 oid [ \_ NIC \_ 交换机 \_ 自由 \_ VF](./oid-nic-switch-free-vf.md)的 oid 设置请求释放资源。

本节包括下列主题：

[发出 OID \_ NIC \_ 交换机 \_ 免费 \_ VF 请求](issuing-oid-nic-switch-allocate-vf-requests.md)

[处理 OID \_ NIC \_ 交换机 \_ 免费 \_ VF 请求](handling-oid-nic-switch-allocate-vf-requests.md)

 

