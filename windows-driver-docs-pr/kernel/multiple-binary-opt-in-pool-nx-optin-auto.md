---
title: 多个二进制 Opt-In POOL_NX_OPTIN_AUTO
description: 如果你是提供不同版本 Windows 的不同驱动程序二进制文件的硬件供应商，则可以使用 POOL_NX_OPTIN_AUTO 选择加入机制。
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 586163aa95f7612628abe4ec2a92baf151bd8169
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96838023"
---
# <a name="multiple-binary-opt-in-pool_nx_optin_auto"></a>多个二进制选择加入：池 \_ NX \_ OPTIN \_ 自动


如果你是提供不同版本 Windows 的不同驱动程序二进制文件的硬件供应商，则可以使用 POOL \_ NX \_ OPTIN \_ 自动选择机制。 此移植助手为 Windows 8 和您的驱动程序支持的每个早期版本的 Windows 构建单独的驱动程序二进制文件。

若要使用此选择加入机制，请 \_ \_ \_ 为要选择的所有源文件定义 POOL NX OPTIN AUTO = 1。 为此，请在驱动程序项目的相应属性页中包含以下预处理器定义：

`C_DEFINES=$(C_DEFINES) -DPOOL_NX_OPTIN_AUTO=1`

对于大多数驱动程序，这种定义足以使选择加入机制为你支持的每个 Windows 版本创建不同的二进制文件。

## <a name="implementation-details"></a>实现详细信息


池 \_ NX \_ OPTIN \_ 自动定义将 **非分页池** 常量名称重新定义为 **NonPagedPoolNx**。 重新定义的池类型仍是编译时常量。 将 **非分页池** 常量名称的实例转换为 **NonPagedPoolNx** 的宏也会将 **NonPagedPoolCacheAligned** 的实例转换为 **NonPagedPoolNxCacheAligned。**

 

 




