---
title: 对 CDB 和探测代码进行预处理和后处理
description: 对 CDB 和探测代码进行预处理和后处理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: 2179292d34d64ecfe5cfdc2b70e968c145a3251a
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96785485"
---
# <a name="pre--and-post-processing-of-cdbs-and-sense-codes"></a>对 CDB 和探测代码进行预处理和后处理


Storport 不会以任何方式验证、拒绝或转换 SCSI 命令描述符 (通过它的 CDBs) 。 同样，也不会筛选或转换从设备收到的检测代码或其他有用数据，以响应因检查条件状态而失败的命令。

 

 




