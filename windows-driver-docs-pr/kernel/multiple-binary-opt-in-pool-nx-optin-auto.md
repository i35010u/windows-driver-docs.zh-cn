---
title: 多个二进制参加 POOL_NX_OPTIN_AUTO
description: 如果您的硬件供应商提供不同的驱动程序二进制文件的不同版本的 Windows，您可以使用 POOL_NX_OPTIN_AUTO 参加机制。
ms.assetid: 5E6759E3-3AF8-4427-BDD0-DB64B3D480A1
ms.localizationpriority: medium
ms.date: 10/17/2018
ms.openlocfilehash: 35bfdd62da933142cabb4fe4e05f60074be83887
ms.sourcegitcommit: a33b7978e22d5bb9f65ca7056f955319049a2e4c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/31/2019
ms.locfileid: "56526950"
---
# <a name="multiple-binary-opt-in-poolnxoptinauto"></a>多个二进制参加：POOL\_NX\_OPTIN\_AUTO


如果您的硬件供应商提供不同的驱动程序二进制文件的不同版本的 Windows，您可以使用池中\_NX\_OPTIN\_自动选择机制。 对 Windows 8 和 Windows 驱动程序支持的每个早期版本，此移植帮助生成单独的驱动程序二进制文件。

若要使用此选择机制，定义池\_NX\_OPTIN\_自动 = 1 的所有源你想要参加的文件。 若要执行此操作，包括驱动程序项目的相应的属性页中的以下预处理器定义：

`C_DEFINES=$(C_DEFINES) -DPOOL_NX_OPTIN_AUTO=1`

对于大多数驱动程序，此定义就足以启用选择的机制来创建每个版本的 Windows 支持不同的二进制文件。

## <a name="implementation-details"></a>实现详细信息


在池中\_NX\_OPTIN\_自动定义重新定义**非分页池**常量名称**NonPagedPoolNx**。 重新定义的池类型仍是一个编译时常量。 实例之间进行转换的宏**非分页池**常量名称到**NonPagedPoolNx**也会将转换的实例**NonPagedPoolCacheAligned**到**NonPagedPoolNxCacheAligned。**

 

 




