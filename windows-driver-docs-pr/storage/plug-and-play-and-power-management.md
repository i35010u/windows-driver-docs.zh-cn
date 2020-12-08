---
title: 即插即用和电源管理
description: 即插即用和电源管理
ms.date: 04/20/2017
ms.localizationpriority: medium
ms.openlocfilehash: a4cb38ae1dfb878a59657bdd23c014f5a7552a20
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96817983"
---
# <a name="plug-and-play-and-power-management"></a>即插即用和电源管理


LsiU3AdapterControl 例程允许无需更改其 HW \_ 初始化数据结构即可实现特殊的适配器控制例程 \_ 。 它包含对 StopAdapter 和 ScsiRestartAdapter ControlTypes 的支持，此功能可将适配器的 HwFindAdapter 和 HwInitialize 例程替换为经过电源管理的周期。 此外，LsiU3StartIo 例程还添加了对 SRBs 的处理，并将函数代码 SRB \_ 函数 \_ 用于 HBA 关闭。

 

 




