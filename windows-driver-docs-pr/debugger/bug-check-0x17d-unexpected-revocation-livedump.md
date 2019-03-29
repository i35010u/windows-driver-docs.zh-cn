---
title: Bug 检查 0x17D PDC_UNEXPECTED_REVOCATION_LIVEDUMP
description: PDC_UNEXPECTED_REVOCATION_LIVEDUMP bug 检查具有 0x0000017D 值。 它表示已被意外吊销激活器。
keywords:
- Bug 检查 0x17D PDC_UNEXPECTED_REVOCATION_LIVEDUMP
- PDC_UNEXPECTED_REVOCATION_LIVEDUMP
ms.date: 01/04/2019
topic_type:
- apiref
api_name:
- PDC_UNEXPECTED_REVOCATION_LIVEDUMP
api_type:
- NA
ms.localizationpriority: medium
ms.openlocfilehash: e5d54509fb6141a6bda5d584c5e6b3e061ebe886
ms.sourcegitcommit: ece0a2affa08f1b6446368ede06040b3153aaae2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/23/2019
ms.locfileid: "56743586"
---
# <a name="bug-check-0x17d-pdcunexpectedrevocationlivedump"></a>Bug 检查 0x17D:PDC\_意外\_吊销\_LIVEDUMP

PDC\_意外\_吊销\_LIVEDUMP bug 检查的值为 0x0000017D。 它表示已被意外吊销激活器。

**重要**本主题适用于程序员。 如果你已使用计算机时收到一个蓝色的屏幕，错误代码的客户，请参阅[疑难解答蓝屏错误](https://windows.microsoft.com/windows-10/troubleshoot-blue-screen-errors)。


 ## <a name="pdcunexpectedrevocationlivedump-parameters"></a>PDC\_意外\_吊销\_LIVEDUMP 参数

|参数|描述|
|--- |--- |
|1| 已吊销的激活器客户端 ID。|
|2| 已吊销的激活器客户端。 |
|3| 已吊销的激活实例中。|
|4| pdc!_PDC_CLIENT_PROCESS_INFO |


## <a name="cause"></a>原因
-----

激活器已被意外吊销。

Livedump 旨在提供信息来调查。

（此代码可以永远不会用于实际的执行错误检查。）



## <a name="see-also"></a>请参阅
----------

[Bug 检查代码参考](bug-check-code-reference2.md)

 




