---
title: SRB \_ 获取 \_ 数据 \_ 格式
description: SRB \_ 获取 \_ 数据 \_ 格式
ms.date: 11/28/2017
ms.localizationpriority: medium
ms.openlocfilehash: 03b0e5b396f4002f7249f0f573596e1a73d61719
ms.sourcegitcommit: 418e6617e2a695c9cb4b37b5b60e264760858acd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/07/2020
ms.locfileid: "96802139"
---
# <a name="srb_get_data_format"></a>SRB \_ 获取 \_ 数据 \_ 格式


## <span id="ddk_srb_get_data_format_ks"></span><span id="DDK_SRB_GET_DATA_FORMAT_KS"></span>


类驱动程序发出此请求以查询流的数据格式。 微型驱动程序应将 *pSrb* - &gt; **CommandData** 设置为流的当前数据格式。

有关数据格式的详细信息，请参阅 [Stream 类微型驱动程序 Design Guide](./streaming-minidrivers2.md)。

 

